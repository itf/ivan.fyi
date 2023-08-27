---
title: Scan notes with laptop webcam

date: 2018-09-16
updated: 2020-07-26
taxonomies:
    tags: [blog,]
---

I was solving a pset, and realized that I needed to draw a graph by hand and include it in my solution. I didn't want to deal with taking a picture with my phone and sending the picture to my computer in order to use it. I wanted to be able to quickly scan it using my webcam. 

So I decided to write a scrip to just do that, I press Ctrl-Print and the magic happens!

It sets my screen brightness to max. Takes a pic with my webcam. Sets the screen brightness to where it was.  Prompts me to crop the picture it took. Uses [textcleaner](http://www.fmwconcepts.com/imagemagick/textcleaner/index.php) to clean the picture up. And at last, it automatically inserts the picture in my org document, and displays the picture.

In other words, a quick and dirty scanner with computer screen flash to scan papers.


# Controlling the brightness

First I needed to allow me to control the brightness without sudo. Here I added my group as a group with permissions to edit the brightness.

    sudo chgrp ivanaf /sys/class/backlight/intel_backlight/brightness
    sudo /bin/chmod g+w  /sys/class/backlight/intel_backlight/brightness

Then I could just use 

    echo brightness /sys/class/backlight/intel_backlight/brightness


# Taking the picture

I use pygame to take the picture.

  ```python
  import pygame
    import pygame.camera
    from pygame.locals import *
    import sys
    from PIL import Image
    import os
    from time import time
    import numpy as np
    
    
    DEVICE = "/dev/video1"
    SIZE = (1280, 720)
    
    #https://www.pyimagesearch.com/2015/09/07/blur-detection-with-opencv/
    
    #try:
    if True:
        import cv2
        has_cv = True
    
        def variance_of_laplacian(image):
            # compute the Laplacian of the image and then return the focus
            # measure, which is simply the variance of the Laplacian
            ans =  cv2.Laplacian(image, cv2.CV_64F).var()
    
            print(ans)
            return cv2.Laplacian(image, cv2.CV_64F).var()
    
        def choose_best(image1, image2):
            if variance_of_laplacian(pygame_to_cvimage(image1))>variance_of_laplacian(pygame_to_cvimage(image2)):
                return image1
            return image2
    
        #https://gist.github.com/jpanganiban/3844261
        def pygame_to_cvimage(surface):
            """Convert a pygame surface into a cv image"""
            ## convert to pillow
            pil_string_image = pygame.image.tostring(surface, "RGB", False)
            pil_im = Image.frombytes("RGB", SIZE, pil_string_image)
    
            numpy_image = np.array(pil_im)
            opencv_image = cv2.cvtColor(numpy_image, cv2.COLOR_RGB2BGR) 
            gray = cv2.cvtColor(opencv_image, cv2.COLOR_BGR2GRAY)
            return gray
    
    #except ImportError:
    else:
        has_cv = False
    
        def choose_best(image1, image2):
            return image2
    
    
    
    
    
    
    
    
    
    
    
    #based on https://gist.github.com/snim2/255151
    #and https://www.pygame.org/docs/tut/CameraIntro.html
    
    
    if __name__ == "__main__":
        file_name = str(sys.argv[1]) 
        pygame.init()
        pygame.camera.init()
    
        cam = pygame.camera.Camera(DEVICE, SIZE)
        cam.start()
    
        display = pygame.display.set_mode(SIZE, 0)
        screen = pygame.surface.Surface(SIZE, 0, display)
        begin_time = time()
    
        #Needed for the camera to adjust brightness and focus
        image = cam.get_image()
        while time()-begin_time < 1.1:
            screen = cam.get_image()
            display.blit(screen, (0,0))
            pygame.display.flip()
            image = choose_best(image, screen)
        
        cam.stop()
    
        pil_string_image = pygame.image.tostring(image,"RGB",False)
        im = Image.frombytes("RGB", SIZE ,pil_string_image)
        
        out_file = open(file_name, 'wb')
        im.save(out_file, "JPEG")
    
    
        #from: http://discourse.techart.online/t/pil-wait-for-image-save/3994/6
    
        out_file.flush()
        os.fsync(out_file)
        out_file.close()
    
        pygame.quit()
```


# Cropping the picture

Again, I use pygame, using the code from these online answers: 
<https://coderwall.com/p/hmp8uw/image-cropping-using-pygame>
<https://stackoverflow.com/questions/6136588/image-cropping-using-python/8696558> 

```python
import pygame
    import pygame.camera
    from pygame.locals import *
    import sys
    from PIL import Image
    import os
    
    #https://coderwall.com/p/hmp8uw/image-cropping-using-pygame
    #https://stackoverflow.com/questions/6136588/image-cropping-using-python/8696558 
    import pygame, sys
    from PIL import Image
    pygame.init()
    
    def displayImage(screen, px, topleft, prior):
        # ensure that the rect always has positive width, height
        x, y = topleft
        width =  pygame.mouse.get_pos()[0] - topleft[0]
        height = pygame.mouse.get_pos()[1] - topleft[1]
        if width < 0:
            x += width
            width = abs(width)
        if height < 0:
            y += height
            height = abs(height)
    
        # eliminate redundant drawing cycles (when mouse isn't moving)
        current = x, y, width, height
        if not (width and height):
            return current
        if current == prior:
            return current
    
        # draw transparent box and blit it onto canvas
        screen.blit(px, px.get_rect())
        im = pygame.Surface((width, height))
        im.fill((128, 128, 128))
        pygame.draw.rect(im, (32, 32, 32), im.get_rect(), 1)
        im.set_alpha(128)
        screen.blit(im, (x, y))
        pygame.display.flip()
    
        # return current box extents
        return (x, y, width, height)
    
    def setup(path):
        px = pygame.image.load(path)
        screen = pygame.display.set_mode( px.get_rect()[2:] )
        screen.blit(px, px.get_rect())
        pygame.display.flip()
        return screen, px
    
    def mainLoop(screen, px):
        topleft = bottomright = prior = None
        n=0
        while n!=1:
            for event in pygame.event.get():
                if event.type == pygame.MOUSEBUTTONUP:
                    if not topleft:
                        topleft = event.pos
                    else:
                        bottomright = event.pos
                        n=1
            if topleft:
                prior = displayImage(screen, px, topleft, prior)
        return ( topleft + bottomright )
    
    if __name__ == "__main__":
        input_loc = str(sys.argv[1]) 
        output_loc = input_loc
        screen, px = setup(input_loc)
        left, upper, right, lower = mainLoop(screen, px)
    
        # ensure output rect always has positive width, height
        if right < left:
            left, right = right, left
        if lower < upper:
            lower, upper = upper, lower
        im = Image.open(input_loc)
        im = im.crop(( left, upper, right, lower))
        pygame.display.quit()
        
        out_file = open(output_loc, 'wb')
        im.save(out_file, "JPEG")
    
    
        #from: http://discourse.techart.online/t/pil-wait-for-image-save/3994/6
        out_file.flush()
        os.fsync(out_file)
        out_file.close()
    
        pygame.quit()
```

# Cleaning the image

To clean the image, I was trying to remove the background by blurring the image, and dividing the original image by the blurred one.

This method is very effective. However, I found something even better, [Fred's ImageMagick Scripts for text cleaning](http://www.fmwconcepts.com/imagemagick/textcleaner/index.php).


# Putting it all together

```el
    (defun ivanaf/org-scan(&optional landscape)
      (interactive)
      (let* ((python-cam-command "~/org/packages/webcamscan/webcam.py")
             (python-crop-command "~/org/packages/webcamscan/crop.py")
             (text-command "~/org/packages/webcamscan/textcleaner")
             (directory "./scan/")
             (file-name (replace-regexp-in-string "\\." "" (format "%s" (float-time))))
             (file-name (concat directory file-name ".jpg"))
             (file-name (expand-file-name file-name))
             (text-args
              (if landscape
                  "-l l -r cw -e normalize -s 1 -f 15 -o 5 -p 5 -u -T"
                "  -r cw -e normalize -s 1 -f 15 -o 5 -p 5 -u -T"))
             (display-brightness-hw "/sys/class/backlight/intel_backlight/brightness")
             (max-brightness "1500")
             (cmd-file-name (shell-quote-argument file-name))
             (brightness (shell-command-to-string (concat "cat " display-brightness-hw)))
             (brightness (replace-regexp-in-string "\n" "" brightness)))
        (make-directory directory t)
        (shell-command (format "echo %s > %s" max-brightness display-brightness-hw))
        (shell-command (format "python3 %s %s" python-cam-command cmd-file-name))
        (shell-command (format "echo %s > %s" brightness display-brightness-hw))
        (shell-command (format "python3 %s %s" python-crop-command cmd-file-name))
        (shell-command (format "%s %s %s %s" text-command text-args cmd-file-name cmd-file-name))
        (insert "\n#+ATTR_ORG: :width 600\n")
        (insert "#+attr_latex: :float nil\n")
        (insert (concat  "#+CAPTION: "  "\n"))
        (insert (concat "[[file:" file-name "][file:" file-name "]]"))
        (org-display-inline-images)))
    
    
    (defun ivanaf/org-scan-l()
      (interactive)
      (ivanaf/org-scan t))
    
    (define-key org-mode-map (kbd "C-<print> ") 'ivanaf/org-scan)
    (define-key org-mode-map (kbd "M-<print> ") 'ivanaf/org-scan-l)
```


# Results:

Here is a "scan" of the back of the mit career fair book from last year, taken in my dark room.

[![img](./jpg/15370864184127958.jpg)](./jpg/15370864184127958.jpg)  

Which is about as good as possible, give the quality of the light / camera. 

