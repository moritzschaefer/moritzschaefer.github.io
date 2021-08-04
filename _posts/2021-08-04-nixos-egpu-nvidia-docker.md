---
layout: single
title:  "Running nvidia-docker on NixOS with an eGPU"
date:   2021-08-04
desc: "Running nvidia-docker on NixOS with an eGPU"
keywords: "egpu,nixos,docker,nvidia,gpu,gpgpu"
categories: [biology,deeplearning]
tags: [biology,structure,gpu,computational,deeplearning]
icon: icon-dna
mathjax: true
---

# Motivation

[AlphaFold](https://github.com/deepmind/alphafold/) 2 has brought unprecented opportunities to the field of (structural) biology. But how to run it with the all imaginable handicaps at once? After some days of debugging, I managed to run AlphaFold2 (and any other GPGPU program** on my EXWM-NixOS using an nvidia-eGPU while having my X-Server still running on my intel GPU. Let's get started.

# Required steps
## eGPU authorization

As explained [here](http://www.pocketnix.org/posts/eGPUs%20under%20Linux%3A%20an%20advanced%20guide), you need to authorize the eGPU such that it is allowed to access you PCIe-bus. This can also be done using the program `bolt`, or in more user-friendly environments like GNOME, a dialog will nicely ask you to authorize after plugging in the eGPU.

```
echo 1 > /sys/bus/thunderbolt/devices/0-0/0-1/authorized
```

## NixOS workarounds

As discussed in this [GitHub issue](https://github.com/NixOS/nixpkgs/issues/131608), there are several Nix-configurations to make.

### Load Nvidia libraries

Intel does not load the required nvidia libraries, so they have to be added manually
```
{ config, ... }:
let
  nvidia_x11 = config.boot.kernelPackages.nvidia_x11;
  nvidia_gl = nvidia_x11.out;
  nvidia_gl_32 = nvidia_x11.lib32;
in
{
  boot.extraModulePackages = [ nvidia_x11 ];
  environment.systemPackages = [ nvidia_x11 ];

  hardware.opengl = {
    enable = true;
    driSupport = true;
    driSupport32Bit = true;
    extraPackages = [ nvidia_gl ];
    extraPackages32 = [ nvidia_gl_32 ];
  };
}
```

### Fix libnvidia-container not finding nvidia-smi and other nvidia binaries.

When running your X-server on intel (internal GPU), nvidia binaries are not propagated in /run/nvida-docker/bin (note: when X-server runs on nvidia, they are linked to /run/nvida-docker/bin from the nix-store (see code)). nvidia-docker looks for the binaries in that folder though. 

This PR works around this issue, by linking the binaries into docker not via the /run/nvidia-docker path, but via the nix-store directly.

https://github.com/NixOS/nixpkgs/pull/132655

The relevant line is the following, patching the lbinvdia-container source code:

```
sed -i "s#/run/nvidia-docker/bin:/run/nvidia-docker/extras/bin#${linuxPackages.nvidia_x11.bin}/origBin#" src/nvc_info.c
```

### Use the fixed version in my NixOS configuration

While this patch is not merged, the following overlay can pull the modified libnvidia-container code into your configuration:

```
    mkNvidiaContainerPkg = { name, containerRuntimePath, configTemplate, additionalPaths ? [] }:
      let
        nvidia-container-runtime = pkgs.callPackage "${inputs.nixpkgs}/pkgs/applications/virtualization/nvidia-container-runtime" {
          inherit containerRuntimePath configTemplate;
        };
      in pkgs.symlinkJoin {
        inherit name;
        paths = [
          # (callPackage ../applications/virtualization/libnvidia-container { })
          (pkgs.callPackage "${inputs.nixpkgs-local}/pkgs/applications/virtualization/libnvidia-container" { })  # this is the patched version
          nvidia-container-runtime
          (pkgs.callPackage "${inputs.nixpkgs}/pkgs/applications/virtualization/nvidia-container-toolkit" {
            inherit nvidia-container-runtime;
          })
        ] ++ additionalPaths;
      };
```


## Configure your X Server to run on intel GPU and to load install nvidia drivers

```
  system.nixos.tags = [ "with-nvidia-egpu" ];

  services.hardware.bolt.enable = true;
  services.xserver.videoDrivers = [ "intel" ];
  boot.extraModulePackages = [ pkgs.linuxPackages.nvidia_x11 ];
  environment.systemPackages = [ pkgs.linuxPackages.nvidia_x11 ];
  boot.blacklistedKernelModules = [ "nouveau" "nvidia_drm" "nvidia_modeset" "nvidia" ];
  # This has been mentioned before in the blog post
  hardware.opengl = {
    enable = true;
    driSupport = true;
    extraPackages = with pkgs; [
      pkgs.linuxPackages.nvidia_x11.out  # required for nvidia-docker
    ];
    extraPackages32 = [ pkgs.linuxPackages.nvidia_x11.lib32 ];
  };
  
  
  # not sure if these are useful/required
  boot.extraModprobeConfig = "options nvidia \"NVreg_DynamicPowerManagement=0x02\"\n";
  services.udev.extraRules = ''
    # Remove NVIDIA USB xHCI Host Controller devices, if present
    ACTION=="add", SUBSYSTEM=="pci", ATTR{vendor}=="0x10de", ATTR{class}=="0x0c0330", ATTR{remove}="1"

    # Remove NVIDIA USB Type-C UCSI devices, if present
    ACTION=="add", SUBSYSTEM=="pci", ATTR{vendor}=="0x10de", ATTR{class}=="0x0c8000", ATTR{remove}="1"

    # Remove NVIDIA Audio devices, if present
    ACTION=="add", SUBSYSTEM=="pci", ATTR{vendor}=="0x10de", ATTR{class}=="0x040300", ATTR{remove}="1"

    # Enable runtime PM for NVIDIA VGA/3D controller devices on driver bind
    ACTION=="bind", SUBSYSTEM=="pci", ATTR{vendor}=="0x10de", ATTR{class}=="0x030000", TEST=="power/control", ATTR{power/control}="auto"
    ACTION=="bind", SUBSYSTEM=="pci", ATTR{vendor}=="0x10de", ATTR{class}=="0x030200", TEST=="power/control", ATTR{power/control}="auto"

    # Disable runtime PM for NVIDIA VGA/3D controller devices on driver unbind
    ACTION=="unbind", SUBSYSTEM=="pci", ATTR{vendor}=="0x10de", ATTR{class}=="0x030000", TEST=="power/control", ATTR{power/control}="on"
    ACTION=="unbind", SUBSYSTEM=="pci", ATTR{vendor}=="0x10de", ATTR{class}=="0x030200", TEST=="power/control", ATTR{power/control}="on"
    '';
```



# Good luck 

