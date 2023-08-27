---
title: Animating gifs in orgmode

date: 2019-05-25
updated: 2019-05-25
taxonomies:
    tags: [blog,]
---
Makes gif animated in orgmode.

From the [org-inline-image package](https://github.com/Fuco1/org-inline-image/blob/master/org-inline-image.el), with minimal modification ( the only change is testing if the figure is an image by checking the 'org-image-overlay, instead of the custom created oerlay). This requires the package dash.

It will automatically play the gif after you've left the (point) on the image. Sadly play gifs seem to be computationally intensive on emacs.
```el
    ;; Copyright (C) 2014 Matus Goljer <matus.goljer@gmail.com>
    ;; Package-requires: ((dash "2.5.0"))
    (defun org-inline-image--get-current-image ()
      "Return the overlay associated with the image under point."
      (car (--select (eq (overlay-get it 'org-image-overlay) t) (overlays-at (point)))))
    
    (defun org-inline-image--get (prop)
      "Return the value of property PROP for image under point."
      (let ((image (org-inline-image--get-current-image)))
        (when image
          (overlay-get image prop))))
    
    (defun org-inline-image-animate ()
      "Animate the image if it's possible."
      (interactive)
      (let ((image-props (org-inline-image--get 'display)))
        (when (image-animated-p image-props)
          (image-animate image-props))))
    
    (defun org-inline-image-animate-auto ()
      (interactive)
      (when (eq 'org-mode major-mode)
        (while-no-input 
          (run-with-idle-timer 0.3 nil 'org-inline-image-animate))))
    
    (setq org-inline-image--get-current-image (byte-compile 'org-inline-image--get-current-image))
    (setq org-inline-image-animate  (byte-compile 'org-inline-image-animate ))
    (add-hook 'post-command-hook 'org-inline-image-animate-auto)
```

