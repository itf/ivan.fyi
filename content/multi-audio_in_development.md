---
title: Multi-audio (In development)

date: 2018-01-21
updated: 2020-07-26
taxonomies:
    tags: [tech,]
---

I enjoy [binaural](https://en.wikipedia.org/wiki/Binaural_recording)
audio. If you don't know what I'm talking about, I'd recommend putting
on headphones and listening to the
[virtual barber shop](https://www.youtube.com/watch?v=IUDTlvagjJA).


# What makes audio binaural?

In few words, you can detect from which location a sound is coming from
by detecting the delay (difference in phase) between the ears, which can
reach $\frac{25cm}{330m/s} \approx 0.8ms$. However, we can localize the
source of a sound in 3 dimensions and the difference in phase only
provides us with one constraint. The rest of the information comes from
how frequencies are absorbed by the head, outer ear and body are
direction dependent; as well as the difference in audio intensity
between the ears.


# Programs that use HRTF

The response of each ear based on the direction of the sound is called
[Head-related transfer function (hrtf)](https://en.wikipedia.org/wiki/Head-related_transfer_function). Multiple programs can make use of HRTF in
order to localize a sound source. Games that use
[openal](https://www.openal.org/) usually have a setting to activate
HRTF if you are using headphones. One example of such game is Minecraft.
Another program is
[pulseaudio](https://www.reddit.com/r/linux_gaming/comments/2ot5ov/enable_system_wide_hrtf_with_pulseaudio/).
It allows you to convert 5.1 audio into binaural audio by localizing the
sound that would come from each of the speakers. This makes watching
movies with a headphone a fairly pleasing experience.


# Basic idea

It is easy to set up audio pipes using jack. I usually install
[Cadence](http://kxstudio.linuxaudio.org/Applications:Cadence) to do
so, since it is extremely user friendly. Therefore, if I can setup a
simple jack application that uses a simple GUI to decide the location of
an audio source and then play the audio on headphones, it should allow
me to do things such as multiaudio or having some sound sound like it is
moving around me.


# About the tools



## [JACK](http://www.jackaudio.org/)

([Cadence](http://kxstudio.linuxaudio.org/Applications:Cadence))

:CUSTOM\_ID: jack-cadence

> JACK (JACK Audio Connection Kit) refers to an API and two
> implementations of this API, jack1 and jack2. It provides a basic
> infrastructure for audio applications to communicate with each other
> and with audio hardware. Through JACK, users are enabled to build
> powerful systems for signal processing and music production.

In other words, Jack provides an easy way to connect the audio from one
application to another. Using its C++ library we can easily make a
client that can take interface with the audio from other applications.

> Cadence is a set of tools useful for audio production.

Cadence is a set of tools that make using JACK much easier. I have never
been able to install JACK, nor use it without installing Cadence.


## [Zita Convolver](https://directory.fsf.org/wiki/Zita-convolver)

Install from libzita-convolver.

> Zita convolver is a C++ library implementing a real-time convolution
> matrix for up to 64 inputs and outputs. It uses multiple partition
> sizes to provide both low delay and efficient CPU use.

In other words, Zita Convolver is a very fast and simple way to apply an
impulse response to audio!


## [QT](https://www.qt.io/)

I wanted the tool to have a gui. QT is one that is cross-platform.

