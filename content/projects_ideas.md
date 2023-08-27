---
title: Projects ideas

date: 2020-07-23
updated: 2020-09-07
tags:
---
A very disorganized list of projects I want to work on, together with notes about them (mostly links with related info)


# Cutting vegetables with blood

Pictures of knives cutting vegetable while drenched in fake blood. No real purpose for this, except that I think it would be cool


# Tep as a pirateshipe navigating through places:

Tep has a helm in a room that looks like a pirateship. It would be really cool if it was connected to something online, such that it seemed that tEp was a real pirate ship.

The idea would be to have a website using open street map together with open layers 

<https://news.ycombinator.com/item?id=23722133>
maybe use open layers on toip of open street map


# Cli picture tools with gui

There are lots of really cool picture effects that only have a terminal interface.  It would be exciting to have a program that could be used for automatically generating previews for those tools by running it with smaller image sizes.


# Primitive images:

This project is really cool, but I don't like the loss function used by it, so instead use a laplacian pyramid loss for the gradient descent.
<https://github.com/fogleman/primitive>

So the same project, but instead of using this loss function, use one based on laplacian pyramids contrast as done by macrofusion.

Maybe make it available online,
<https://github.com/silvia-odwyer/photon>

seems like a good option! Specially if combined with:
<https://github.com/silvia-odwyer/gld>

Probably use laplacian pyramid loss for the descent. There are some articles about it online.

this one does 


# Music lyrics video for danger line

The lyrics are displayed while moving around a "red line" . The "danger line" is the body outline of someone who died (red), but you only discover it is the outline of the body at the end of the song.

Throughout the song the lyrics go around the outline

Until the very end, they are generally outside the outline, but certain words can be on the boundary (the inside of the boundary represents death). Some words might be in the other side of the boundary.

The effect of bullet Hole, is zooming inside O of hole and inside it there is another hole, to give the impression of going through.

Maybe some effect of heartbeats ecg during the solos.

Once you are inside the outline, things get a lot redder, like red border.

Daugther brings you further from the line


# 3d online game of walking around east campus with the murals

Maybe allow people to upload pictures?

I'd really enjoy to have a 3d representation of the inside of EastCampus, with all the murals and all.
<https://learn.display.land/capturing-reality>

display.land would be ideal, but it was discontinued on July 10 2020.

(Display.land is an interesting 3D scanning and modeling app built around Google’s ARCore augmented reality processing. The app allows you to scan objects in 3D and then edit, export, or share your scans, all for free!)
<https://developers.google.com/ar/develop/java/quickstart>

<https://3dscanexpert.com/scann3d-android-photogrammetry-app-review/>

<https://3dscanexpert.com/free-3d-scanning-video-smartphone/>


# Route panorama on android

I want to implement an app that performs route panoramas on android.

Here are some link ideas.
<https://en.wikipedia.org/wiki/Route_panorama>
<https://www.cs.iupui.edu/~jzheng/RP/>

And maybe strip/slip photography:
<https://en.wikipedia.org/wiki/Strip_photography>

<https://github.com/duanhong169/Camera>

<https://github.com/CameraKit/camerakit-android>


# Dating website where you ship your friends


# Super resolution photo app by upsampling alignning and enfusing or merging, for astrophotography

<https://petapixel.com/2015/02/21/a-practical-guide-to-creating-superresolution-photos-with-photoshop/>
<https://groups.google.com/g/hugin-ptx/c/ijOCcBX7me8>
<http://www.astrosurf.com/cidadao/super.htm>


# selfie with longer focal distance by combining multiple close shots

By scanning your face (similarly to a route panorama), fake your lens to have a longer focal distance, while improving blurring the background

idea: use gyroscope to put a dot on the screen that force the video to stay in the same plane. Use maybe motion tracking:
<https://source.android.com/devices/camera/motion-tracking>


# Photogrammetry of street art tutorial

start:
<https://medium.com/realities-io/getting-started-with-photogrammetry-d0a6ee40cb72>
video for the above:
<https://www.youtube.com/watch?v=doiimSnLOBM>
also <http://azadux.com/everydayascan>

Also this guy did a lot of it, but left no instructions:
<https://www.youtube.com/watch?v=IrgyUFkeJOY>

sketchfab seems to be the correct place to share it.

<https://news.ycombinator.com/item?id=19685891>

<https://ww.reddit.com/r/3Dprinting/comments/87tk4j/3d_scanning_with_just_a_phonecamera/>

with colmap
also <https://www.youtube.com/watch?v=bDHJM6nAKtc>


# cindyjs

<https://cindyjs.org/docs/>
<https://montaga.github.io/spherical/>
Just play with some spherical droste effects with pictures from mit
<https://arxiv.org/pdf/1605.01396.pdf>

Also map picture into sphere by using reflections/tiling? 
Idea: convert rectangle to circle conformally, followed by identifying it with one of the hemispheres of a stereographic transformation
<https://arxiv.org/pdf/1509.06344.pdf>

Or maybe assume it is peirce quincucial
<https://arxiv.org/pdf/1605.01396.pdf>

<https://mipav.cit.nih.gov/pubwiki/index.php/Transform:_Conformal_Mapping_Algorithms#Transformation:_Circle_to_Rectangle>

<https://www.osti.gov/servlets/purl/4800477>
<https://www.osti.gov/biblio/4800477-conformal-mapping-circle-onto-rectangle> 


# Plausible analytics for MIT/sipb

<https://plausible.io/blog/self-hosted-web-analytics-beta>


# Make pictures boring

Detects what is relevant in a picture and removes it.
<https://www.immersivelimit.com/tutorials/yolact-with-google-colab>
<https://kharshit.github.io/blog/2019/08/23/quick-intro-to-instance-segmentation>

use instance segmentation to detect what is interesting

The use this to fill it up:
<https://github.com/zavolokas/Inpainting>
<https://github.com/YuanTingHsieh/Image_Completion>


# Quaternions exploration

Have a simple 3d scene. Apply quaternion functions to the positions of the points. Find an equivalent to droste effect but in 3d space

Similar to this demo <https://montaga.github.io/spherical/>
So more like this: <https://eater.net/quaternions/video/intro>

But with a more complex 3d scene and allowing more things than rotations, i.e. allowing complex functions in terms of the quaternion that defines the position.

Using a ray marcher <https://github.com/HackerPoet/PySpace> might be worth it to have some visualizations that use fractals,

Or maybe just use <https://cindyjs.org/docs/cindygltutorial/rendering3d.html>.

We will effectively be using conformal transformations
<https://mathoverflow.net/questions/52209/3d-conformal-mappings>

It seems that the only types are inversion, translation, rotation and dilation. 

maybe use this for the visualization: <https://www.youtube.com/watch?v=ztsi0CLxmjw>, same thing used for exploring hyperbolic space.

Also, I want everything to happen on the surface of a 4d sphere.

Just more information about quarenions <https://marctenbosch.com/quaternions/> < maybe quaternions are trash

<https://arxiv.org/abs/1605.01396>


## Exploring surface of 4d objects.

You yourself is like a cube, so you see infinite copies of you on the distance

maybe use a non euclidean ray tracer
<https://www.youtube.com/watch?v=YvU-srHhQxw>

<https://github.com/Limeth/euclider>

<https://www.youtube.com/watch?v=tl40xidKF-4>

but I kinda wnat it to be in javascript

or maybe like: <https://arxiv.org/abs/2002.09533>  ->> sounds really really promising / seems to be already doing it. <https://www.youtube.com/user/ZenoTheRogue>
<https://ww.reddit.com/r/rust/comments/88b6ix/euclider_noneuclidean_raytracing_prototype/>
<https://twitter.com/zenorogue/status/1245367263936512001>  


# Just add some posts playing with js here

<https://ew.reddit.com/r/orgmode/comments/5bi6ku/tip_for_exporting_javascript_source_block_to/>


# Make music using this imo problem solution

<https://www.youtube.com/watch?v=M64HUIJFTZM>


# toilet measure weight

You sit on the toilet. It shows you your weight.


# Practice retouching face images

<https://patdavid.net/2011/12/getting-around-in-gimp-skin-retouching.html>
<https://patdavid.net/2013/08/an-open-source-headshot-ronni_21.html>


# Pagination for my blog

Pagination for this org mode blog


# RSS for this blog


# Better theme for this blog, make it not ugly


# Use seam carving to split a image into puzzle pieces for cutting

<https://www.youtube.com/watch?v=6NcIJXTlugc>


# Add my emacs packages to melpa

<https://github.com/melpa/melpa>


# Random notes


## AR core for android

<https://www.youtube.com/watch?v=Mzr3MVzSjSM>
<https://github.com/lvonasek/tango/wiki/3D-Scanner-for-ARcore>

<https://github.com/googlesamples/arcore-depth-lab>
<https://www.youtube.com/watch?v=Mzr3MVzSjSM>


# Play with some pre trained CNN

<https://www.analyticsvidhya.com/blog/2018/07/top-10-pretrained-models-get-started-deep-learning-part-1-computer-vision/>


# Click to expand table of contents

<https://codepen.io/peternguyen/pen/hICga>

From: <https://codepen.io/peternguyen/pen/hICga>

     <input id="toggle" style="display: none; visibility: hidden;" type="checkbox" checked>
      <label for="toggle">Table of contents</label>
      <div id="expand">
     Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas porta non turpis faucibus lobortis. Curabitur non eros rutrum, gravida felis non, luctus velit. Ut commodo congue velit feugiat lobortis. Etiam nec dolor quis nulla bibendum blandit vitae nec enim. Maecenas id dignissim erat. Aenean ac mi nec ante venenatis interdum quis vel lacus.
     </div>
    #expand {
      height: auto;
      visibility: hidden;
      display: block;
      height: 0em;
      overflow: hidden;
      transition: max-height 0.3s linear, visibility 0.65s ease;
    }
    #toggle:checked ~ #expand {
      height: auto;
      display: block;
    	overflow: auto; 
      visibility:  visible;
      transition: max-height 0.3s linear, visibility 0.65s ease;
    }

    (defun org-export-head--custom-toc-input(depth info &optional scope)
      (let ((toc-entries
    	 (mapcar (lambda (headline)
    		   (cons (org-html--format-toc-headline headline info)
    			 (org-export-get-relative-level headline info)))
    		 (org-export-collect-headlines info depth scope))))
        (when toc-entries
          (let ((toc (concat "<nav id=\"table-of-contents\">\n" 
                      "<input id=\"toggle-toc\" style=\"display: none; visibility: hidden;\" type=\"checkbox\">\n"
                      "<label for=\"toggle-toc\">\n <h2> <a> Table of Contents </a> </h2>\n </label>\n"
                      "<div id=\"text-table-of-contents\">"
    			 (org-html--toc-text toc-entries)
    			 "</div>\n"
                             "</nav> \n")))
            toc))))

    #table-of-contents #text-table-of-contents{
      visibility: hidden;
      display: block;
      height: 0em;
      overflow: hidden;
    }
    
    #table-of-contents #toggle-toc:checked ~ #text-table-of-contents {
      height: auto;
      display: block;
            overflow: auto; 
      visibility:  visible;
    }
    
    #table-of-contents h2 b{
        cursor: pointer;
        border-bottom:1px dotted;
    }
    #table-of-contents h2{
        cursor: pointer;
    }

    (defun org-export-head--custom-toc(depth info &optional scope)
      (let ((toc-entries
    	 (mapcar (lambda (headline)
    		   (cons (org-html--format-toc-headline headline info)
    			 (org-export-get-relative-level headline info)))
    		 (org-export-collect-headlines info depth scope))))
        (when toc-entries
          (let ((toc (concat "<nav id=\"table-of-contents\">\n"
                             "<a href=\"#text-table-of-contents\">\n <h2> <b>Table of Contents </b> </h2>\n </a>\n"
                             "<div id=\"text-table-of-contents\">"
    			 (org-html--toc-text toc-entries)
    			 "</div>\n"
                             "</nav> \n")))
            toc))))

    #something {
      display: none;
    }
    
    #something:target {
      display: block;
    }


# Better TOC for tags page

<https://www.lycarter.com/tags/> 


# Keep state about displaying comments

<https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API>

