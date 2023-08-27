---
title: Emacs Tramp asking for password

date: 2019-05-21
updated: 2019-05-23
taxonomies:
    tags: [tech,]
---
For about a week, every time I initialized emacs, Tramp would constantly ask for my password, both for `sudo` and for `ssh`.

This means that in the recent file list there is a sudo file or a ssh file, and everytime emacs initialize, it is trying to load this list (which requires it to re-ask for the password if it is not saved). 

If this happens to you, the easiest fix is to clean the recent file lists by running:
```el
    (setq session-file-alist ())
    (setq file-name-history ())

```