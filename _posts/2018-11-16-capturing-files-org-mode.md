---
layout: single
title:  "Capturing files with org-mode"
date:   2018-11-16
desc: "Emacs org-mode is great for capturing quick notes, links and similiar text based resources. However sometimes it can come in handy to store or archive a file"
keywords: "emacs,automation,org-mode"
categories: [Tools]
tags: [emacs,automation,org-mode]
icon: icon-file-upload
---


Emacs' org-mode is a fascinating tool to document, plan, structure and archive daily tasks, texts and todos. The org-capture command is at the core of, well, capturing new items into your organized storage. However it lacks the ability to automatically add files to these items. 

Two example that occur to me on a regular basis is archiving documents and receipts. For both I use my smartphone camera (except for highly important documents) with an App that automatically detects the paper on the image, cuts it out and applies color corrections to make it look like a real scan. All my camera images are synced to my computer (I use Seafile for this, which is an open-source clone of Dropbox), so to archive such a scan (in contrast to losing it in the stream of hundreds of photos I take with my smartphone) it would be nice to have an org-capture template that 

1. Creates a new entry in a file dedicated to receipts or documents
2. Copies the most recently created file from my "synchronised photos folder" to my "org-mode directory" and attach it to the new-entry
3. Add a link to the entry that points to the attached file, such that it can be shown in the org file (org-toggle-inline-images)

Here is how I achieved this:

### Use an ordinary capture template to create a new item for a receipt

```
(custom-set-variables
 '(org-capture-templates
   (quote
     ("r" "Receipt" entry
      (file+olp+datetree "~/wiki/receipts.org")
      "* %?"
      )
    )))
  )
 ``` 

### Set a hook to postprocess captured items

```
(add-hook 'org-capture-before-finalize-hook 'moritzs/download-smartphone-photo)
```

### Make sure only receipts capture items are modified and attach the most recently synced file to them


```

(defun moritzs/download-smartphone-photo ()
  (when (equal (buffer-name) "CAPTURE-receipts.org")
    (newline)
    (org-download-image (moritzs/recent-smartphone-photo))
    ))
```

org-download comes in handy when attaching files and adding links in your org files. To make org-download use org-attach instead of copying the files straight into your directories set 

```
(setq org-download-method 'attach)
```

### Find the most recently synced file

```
(defun moritzs/recent-smartphone-photo ()
  "Open a recently taken smartphone picture."
  (format "/home/moritz/Seafile/Main/My Photos/Camera/%s" (shell-command-to-string "ls -t  '/home/moritz/Seafile/Main/My Photos/Camera/' | head -n 1 | tr -d '\n'"))
  )
```

## Weaknesses

The elisp code is not polished (for example one could use variables to express the directories in order to not repeat them).

Furthermore this strategy follows a strict protocol of 

- Taking an image
- Waiting until synchronization is complete
- Capturing with org-capture

If you have an idea, or implemented a more flexible strategy to solve this problem, let me know in the comments or on twitter (@muronglizi).
