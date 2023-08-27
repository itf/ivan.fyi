---
title: Emacs drag-drop pdfs, paste html, custom templates

date: 2018-08-19
updated: 2020-07-26
taxonomies:
    tags: [blog,]
---


# UPDATE:

This documents my first experience with programming in elisp. In restrospect, I was really bad at it. This post then shows that you can still make something with elisp even if you are bad at it.

A slightly better example of making something with elisp is on my package clipboard2org, a tiny package to paste html or picture. See [clipboard2org](https://github.com/itf/clipboard2org/blob/master/clipboard2org.el)


# PDF files drag-drop

I wanted to be able to drag and drop pdf files, as well as drag and drop
pdf URLs to emacs. The result of dragging should be to download the file
to a directory under the same directory as the org file you are editing
and then create a link to the file. It also allows for drag and drop of
image files.

The code was based on [org download](https://github.com/abo-abo/org-download). If it is not a pdf, or if it is but the download fails, it
fails back to the original drag and drop code.
```el
    (defun org-file-copy-pdf (fname)
      (let* ((path (substring fname 5))
             (org-file-pdf-directory "./pdflib")
             (name (file-name-nondirectory (file-name-sans-extension path))))
        (make-directory org-file-pdf-directory :parents)
        (condition-case nill
            (copy-file (dnd-unescape-uri path) (expand-file-name (format "%s.pdf" name) org-file-pdf-directory))
          (error
           ())
          )
        (file-relative-name (expand-file-name (format "%s.pdf" name) org-file-pdf-directory) "./"))
      )
    
    (defun org-file-insert (fname)
      (let* ((img-regexp "\\([pP][nN][gG]\\|[jJ][pP][eE]?[gG]\\)\\>")
             (pdf-regexp  "\\([pP][dD][fF]\\)\\>"))
        (cond  
         ((string-match img-regexp fname)
          (insert "#+ATTR_ORG: :width 300\n")
          (insert (concat  "#+CAPTION: "  "\n"))
          (insert (format "[[%s]]" fname))
          (org-display-inline-images t t))
         ((string-match pdf-regexp fname)
          (insert (format "[[file:%s][%s]]\n"  (org-file-copy-pdf fname) (file-name-nondirectory (file-name-sans-extension path)))))
         (t (insert (format "[[%s]]\n" fname))
            )
         )
        )
      )
    
    (defun org-file-dnd-fallback (uri action)
      (let ((dnd-protocol-alist
             (rassq-delete-all
              'org-file-dnd-protocol
              (copy-alist dnd-protocol-alist))))
        (dnd-handle-one-url nil action uri)))
    
    (defun org-file-dnd-protocol (uri action)
      (cond ((eq major-mode 'org-mode)
             (condition-case nil
                 (org-file-insert uri)
               (error
                (org-file-dnd-fallback uri action))))
            (t
             (org-file-dnd-fallback uri action))))
    
    
    (add-to-list 'dnd-protocol-alist '("^file:" .  org-file-dnd-protocol))
    
    
    (require 'url)
    
    (defun org-file-pdf-url-insert (url)
      (let* ((org-file-pdf-directory "./pdflib")
             (name (file-name-nondirectory url))
             (path (expand-file-name (file-name-nondirectory url) org-file-pdf-directory))
             (relative-path (file-relative-name path "./")))
        (make-directory org-file-pdf-directory :parents)
        (url-copy-file url path t)
        (insert (format "[[file:%s][%s]]\n"  relative-path name)))
      )
    
    (defun org-file-pdf-url-dnd-fallback (uri action)
      (let ((dnd-protocol-alist
             (rassq-delete-all
              'org-file-pdf-url-dnd-protocol
              (copy-alist dnd-protocol-alist))))
        (dnd-handle-one-url nil action uri)))
    
    (defun org-file-pdf-url-dnd-protocol (uri action)
      (cond ((eq major-mode 'org-mode)
             (condition-case nil
                 (org-file-pdf-url-insert uri)
               (error
                (org-file-pdf-url-dnd-fallback uri action))))
            (t
             (org-file-pdf-url-dnd-fallback uri action))))
    
    
    (add-to-list 'dnd-protocol-alist '("^https?.*\\.pdf" .  org-file-pdf-url-dnd-protocol))
```


# Custom easy templates

Easy templates cannot run arbitrary code. They are handled by org-cycle,
which is a function that handles every action that TAB performs in org
mode.

So, I created a function and added an advice to org-cycle, This detects
strings of the type "`>[a-zA-Z]+`", i.e. > followed by letters and then
runs a function.

In order to create other templates, add another block similar to

```el
    ((string= key "t")
    (insert-todays-date)
    t)
```

under it.

This particular template inserts today's date when someone writes >t and
presses tab.
```el
    (defun insert-todays-date ()
      (interactive)
      (insert (format-time-string "<%Y-%m-%d>")))
    
    (defun org-try-my-template-function (&optional arg)
        "Try to complete a structure template before point.
    This looks for strings like \"<e\" on an otherwise empty line and
    expands them."
        (interactive)
        (let ((l (buffer-substring (point-at-bol) (point)))
          a)
          (if (and (looking-at "[ \t]*$")
               (string-match "^[ \t]*>\\([a-zA-Z]+\\)$" l))
              (let* ((key (match-string 1 l))
                     (start  (point-at-bol))
                     (end (point)))
                (when
                    (cond
                     ((string= key "t")
                      (insert-todays-date)
                      t)
                     )
                  (delete-region start end)
                  t)
                ))))
    
    
    (require 'org)
    (with-eval-after-load 'org 
      (advice-add #'org-cycle :before-until   #' org-try-my-template-function))
```

# Pasting HTML in org mode

This was inspired by
[this stack overflow question](https://emacs.stackexchange.com/questions/12121/org-mode-parsing-rich-html-directly-when-pasting). It suggested using `xclip` to access the
clipboard.

The problem is that `xclip` causes emacs to hang, because it forks a
child that keeps stdout open. So instead, one can use the emacs backed
for getting the xselection from the clipboard.

This code requests a text/html selection and checks if it exists. If it
exists, it first decodes it using whatever encoding was being used, and
then uses pandoc to convert the html to org mode.

```el
    (defun html2org-clipboard ()
      "Convert clipboard contents from HTML to Org and then paste (yank)."
      (interactive)
      (let* (
           (text_html (gui-backend-get-selection 'PRIMARY 'text/html))
           (text_raw (gui-get-selection)) 
           (text_html (when text_html
                        (decode-coding-string text_html 'unix)))
           (text_html (when text_html
                        (shell-command-to-string (concat "echo "  (shell-quote-argument text_html) "|timeout 2  pandoc -f html-native_divs-native_spans -t org"))))
           (text (or text_html
                   text_raw))
           )
        (progn  (kill-new text) (yank))))
    
    
    (with-eval-after-load 'org 
      (define-key org-mode-map (kbd "C-y ") 'html2org-clipboard)
      (define-key org-mode-map (kbd "C-<tab>") '(lambda() (interactive) (save-excursion  (org-back-to-heading)
                                                                      (org-cycle))))
      )
```
