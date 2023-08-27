---
title: Export subtree with files

date: 2018-09-13
updated: 2020-07-26
taxonomies:
    tags: [blog,]
---


# Update:

Now this is on on github, in the repo [org-export-with-files](https://github.com/itf/org-export-with-files). It is fairly usable and fairly useful. The next step is to figure out how to best deal with custom links.


# Summary

I have a main org files that contains notes for multiple classes and papers in different headlines. It is very easy to use this org file to find information since every note contains links to the relevant papers.

However, sharing this file with someone can be challenging, since I just want to share the relevant notes/papers and not everything that is linked by this file.

The code below solves this problem. It creates a hard link of every file linked by the specific headline into the export directory and fixes all the links in the exported pdf so that it points to the relative location of those files.

This allows me to quickly generate a folder that contains all the files I wanna share as well as a pdf that allows the other person to easily navigate through the files and see the relevant information.


# Warning:

The file links when exporting to latex need to be of the form [[<file>] [name of the link]]. I other words, they need a description. Links without descriptions are interpreted as images, even if they have extensions such as pdf.


# Code
```el
    (require 'ox)
    
    
    (defun export-with-files-export (&optional directory-name)
      (interactive)
      (let ((directory-name (or directory-name (read-directory-name "Directory:"))))
        (make-directory directory-name t)
        (widen)
        (org-narrow-to-subtree)
        
        ;;Create copy of the 
        (org-export-with-buffer-copy
         (let* ((ast (org-element-parse-buffer)))
           (org-element-map ast 'link
             (lambda (link)
               (export-with-files--fix-file-external-link-ast directory-name link)))
           
           
           ;;Convert the buffer to contain the new AST, 
            ;;this is needed because the exporter expects the content to be in a buffer
           (erase-buffer) 
           (insert (org-element-interpret-data ast))
           
           (outline-show-all)
           (goto-char (point-min))
           (let* ((file-name  (export-with-files--escaped-headline))
                  (new-file-name (concat directory-name file-name)))
             ;; Make the buffer file be in the new directory, because
             ;; org-latex-export-to-pdf always export to the working directory of the buffer
             (set-visited-file-name (concat new-file-name ".org"))
    
             ;; Name of the tex file / pdf file
             (org-set-property
              "EXPORT_FILE_NAME"
              file-name)
             (deactivate-mark)
            (org-latex-export-to-pdf nil t)))))
      (widen))
         
    
    
    (defun export-with-files--fix-file-external-link-ast (directory-path link)
      "Creates hard links to the external files in the output directory"
      (when (string= (org-element-property :type link) "file")
        (let* ((path (org-element-property :path link))
               (extension (file-name-extension path))
               (link-copy (org-element-copy link))
               (img-extensions '("jpg" "tiff" "png" "bmp"))
               (link-description (org-element-contents link))
               ;; Put files in subdirectories with the extension of the file
               (new-relative-path 
                (concat "./" extension "/" (file-name-nondirectory path)))
               (new-hard-link-path (concat directory-path new-relative-path))
               (new-hard-link-directory (file-name-directory new-hard-link-path)))
          
          ;;Fix the AST
          ;;If image, remove description so it will become a real image instead of a link
         (unless (or (member extension img-extensions) (not link-description))
          (apply #'org-element-adopt-elements link-copy link-description))
          (org-element-put-property link-copy :path new-relative-path)
          (org-element-set-element link  link-copy)
          
          ;;Create hard link folder
          (make-directory new-hard-link-directory t)
          ;;Create hard link, not replacing if it already exists, catching error if file does not exist
          (condition-case nil
              (add-name-to-file path new-hard-link-path nil)
            (error nil)))))
    
    
    
    (defun export-with-files--escaped-headline ()
      (export-with-files--escape
       (nth 4 (org-heading-components))))
    
    (defun export-with-files--escape(text)
      (replace-regexp-in-string "[\\?.,!:]" ""
       (replace-regexp-in-string "/" "-" 
        (replace-regexp-in-string " " "_" text))))

```