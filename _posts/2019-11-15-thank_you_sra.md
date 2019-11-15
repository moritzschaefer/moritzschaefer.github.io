* 
---
layout: single
title:  "Thank you fasterq-dump - I learned a lot about filesystems"
date:   2019-11-15
desc: "sra toolkit tmp/temporary cache directory"
keywords: "buffer,sra,toolkit,tmp,problem,cache"
categories: [linux,]
tags: [linux]
icon: icon-default
---
After waiting long hours to download a few SRAs using fastq-dump, I was happy to learn that fasterq-dump would finally lead to faster fastq files on my machine.

Furthermore I ran into a lot of trouble because of temporary/cache files, clogging my disk and making fastq-downloads fail, a problem which I thought would be solved with the added -t option in fasterq-dump. From SRA-tool's online wiki: 

> The location of the temporary directory can be changed too:
> $fasterq-dump SRR000001 -O /mnt/big_hdd -t /tmp/scratch


Mysteriously however, my downloads went on crashing, although I set the temorary directory to my home directory which should have enough storage capacity:

> 2019-11-15T10:33:45 fasterq-dump.2.10.0 err: storage exhausted while writing file within file system module - system bad file descriptor error fd='4'   

Observing disk usage during download of a ~8GB large fastq files showed puzzling results:

After 1 minute of of running fasterq-dump:
> $ df -h
> Filesystem                                     Size  Used Avail Use% Mounted on
> /dev/sda2                                       30G   23G  5.7G  80% /
> /dev/sda4                                      3.3T  2.7T  617G  82% /home
> $ ncdu /
>   12.3GiB [##########] /usr
>    1.3GiB [#         ] /lib
>    1.3GiB [#         ] /opt
>    1.3GiB [#         ] /var
>  199.4MiB [          ] /boot
>   41.7MiB [          ] /root

After ~10 minutes of running fasterq-dump:

> $ df -h
> Filesystem                                     Size  Used Avail Use% Mounted on
> /dev/sda2                                       30G   28G  666M  98% /
> /dev/sda4                                      3.3T  2.7T  605G  82% /home
> $ ncdu /
>   12.3GiB [##########] /usr
>    1.3GiB [#         ] /lib
>    1.3GiB [#         ] /opt
>    1.3GiB [#         ] /var
>  199.4MiB [          ] /boot
>   41.7MiB [          ] /root
>   24.5MiB [          ] /tmp

A change in the disk usage without a change in file sizes could only be explained by deleted, yet still opened files, so I checked open but deleted files and indeed observed an interesting candidate (the only one actually):

> lsof +L1
> COMMAND     PID     USER   FD   TYPE DEVICE   SIZE/OFF NLINK    NODE NAME
> fasterq-d 17854 schamori    7u   REG    8,2 8002551155     0 1179402 /var/tmp/.sra.cache (deleted)

fasterq-dump apparently still allocated a slowly growing sparse file, intended to become ~8GB of size in /var/tmp/.

> $ sudo  debugfs -R 'stat <1179402>' /dev/sda2
> Inode: 1179402   Type: regular    Mode:  0644   Flags: 0x80000
> Generation: 4259928218    Version: 0x00000000:00000001
> User: 30925   Group:   100   Size: 8002551155
> File ACL: 0    Directory ACL: 0
> Links: 0   Blockcount: 468104
> Fragment:  Address: 0    Number: 0    Size: 0
>  ctime: 0x5dce8179:e2d27d90 -- Fri Nov 15 11:44:09 2019
>  atime: 0x5dce8179:e4bac58c -- Fri Nov 15 11:44:09 2019
>  mtime: 0x5dce8179:e2d27d90 -- Fri Nov 15 11:44:09 2019
> crtime: 0x5dce80fb:af533c54 -- Fri Nov 15 11:42:03 2019
> dtime: 0x0011fa28 -- Wed Jan 14 16:15:52 1970
> Size of extra inode fields: 28
> EXTENTS:
> (ETB0):4752581, (0-127):999424-999551, (132-291):999556-999715, (444-507):999868-999931, (632-695):1000056-1000119, (800-863):1000224-1000287, (1000-1063):1000424-1000487, (1196-1259):1000620-1000683, (1352-2047):1000776-1001471, (2048-4095):1294336-1296383 

After several minutes:
> sudo  debugfs -R 'stat <1179402>' /dev/sda2
> Inode: 1179402   Type: regular    Mode:  0644   Flags: 0x80000
> Generation: 4259928218    Version: 0x00000000:00000001
> User: 30925   Group:   100   Size: 8002551155
> File ACL: 0    Directory ACL: 0
> Links: 0   Blockcount: 468104
> Fragment:  Address: 0    Number: 0    Size: 0
>  ctime: 0x5dce8179:e2d27d90 -- Fri Nov 15 11:44:09 2019
>  atime: 0x5dce8179:e4bac58c -- Fri Nov 15 11:44:09 2019
>  mtime: 0x5dce8179:e2d27d90 -- Fri Nov 15 11:44:09 2019
> crtime: 0x5dce80fb:af533c54 -- Fri Nov 15 11:42:03 2019
> dtime: 0x0011fa28 -- Wed Jan 14 16:15:52 1970
> Size of extra inode fields: 28
> EXTENTS:
> (ETB0):4752581, (0-127):999424-999551, (132-291):999556-999715, (444-507):999868-999931, (632-695):1000056-1000119, (800-863):1000224-1000287, (1000-1063):1000424-1000487, (1196-1259):1000620-1000683, (1352-2047):1000776-1001471, (2048-4095):1294336-1296383, (4096-6087):1724416-1726407, (157628-157695):1003452-1003519, (157696-159743):1296384-1298431, (159744-161791):1726464-1728511, (161792-162363):1744896-1745467, (313908-315391):1008180-1009663, (315392-317439):1421312-1423359, (317440-319091):1728512-1730163, (470184-471039):1010856-1011711, (471040-473087):1423360-1425407, (473088-474663):1730560-1732135, (626468-626687):1036068-1036287, (626688-628735):1413120-1415167, (628736-630783):1732608-1734655, (630784-631075):1746944-1747235, (782752-784383):1038752-1040383, (784384-786335):1734656-1736607, (939032-940031):1416216-1417215, (940032-942079):1425408-1427455, (942080-943607):1753088-1754615, (1098492-1099775):1434364-1435647, (1099776-1101823):1427456-1429503, (1101824-1103355):1757184-1758715, (1255196-1255423):1437468-1437695, (1255424-1257471):1417216-1419263, (1257472-1259519):1429504-1431551, (1259520-1261083):1765376-1766939, (1412712-1413119):1300072-1300479, (1413120-1415167):1419264-1421311, (1415168-1417215):1763328-1765375, (1417216-1417575):1767424-1767783, (1589844-1591295):1309268-1310719, (1591296-1593343):1431552-1433599, (1593344-1595391):1740800-1742847, (1595392-1595603):1794048-1794259, (1772048-1773567):1286672-1288191, (1773568-1775615):1742848-1744895, (1775616-1776655):1773568-1774607, (1953732-1953747):1290180-1290195

A short google search lead me to learn about the general caching mechanisms of the SRA toolkit (I should have read the docs just earlier) and how to [quickly manipulate them](https://standage.github.io/that-darn-cache-configuring-the-sra-toolkit.html).


So thank you NCBI/SRA. You've made me learn a lot about the Linux filesystem.
