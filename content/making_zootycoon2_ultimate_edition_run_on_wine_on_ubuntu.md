---
title: Making zootycoon2 ultimate edition run on wine on ubuntu.

date: 2021-01-08
updated: 2021-01-08
taxonomies:
    tags: [games,]
---

To find soundcards on directx you will need:

    winetricks mfc42

For the graphs, you need native directx9

    winetricks directx9

Other information about my current setup: I'm running it in my default wine prefix, (~/.wine), configured to be a 32bit prefix. I've configured this prefix to use Alsa audio, instead of pulseaudio.

I've also installed dxvk (before installing directx9), and since I'm using an intel graphics card

    sudo apt-get install mesa-vulkan-drivers mesa-vulkan-drivers:i386
    sudo apt-get install libvulkan1 libvulkan1:i386

You also need to have the program properly installed in wine. If you somehow have a version that can run without being installed, this will cause it to not find the audiocards.

If you have problems with the windows size, make wine start in windowed mode.

