---
title: vertical3D
type: projects
image: /uploads/2015/07/v3d-ss2_sm.png
socialShare: false
---
The Vertical3D project is a collection of C++ application libaries used across my various 3D application projects. There are libraries for image reading & writing (PNG, TGA, BMP, JPEG), font rendering (bmfont, FreeType), OpenAL audio, basic 3D data types, an event framework, OpenGL rendering helpers, and backend window drivers for SDL, SDL2, FLTK, and SMFL.

### Voxel

![voxel](/uploads/2015/07/voxel.png)

Voxel is a small application created for the purposes of testing out voxel-based random world generation and manipulation a la [Minecraft](//minecraft.net). It is written in C++ using the [Vertical3D Library](https://github.com/farrcraft/vertical3d) components and libnoise for the terrain generation.
[GitHub repo](https://github.com/sigsegv42/voxel)


### Pong!

![pong](/uploads/2015/07/pong.jpg)


A rehash of the classic. Simple 2D graphics using OpenGL and sound effects via OpenAL. Supports 2 player Co-op and single player versus AI game play modes. It began as a simple project to implement a completely finished and working game utilizing modern C++. Since the completion of the working prototype, it has slowly become a test application for a growing set of common framework libraries.


### Tetris

![tetris](/uploads/2015/07/tetris.png)

A rehash of the classic. Simple 2D graphics using OpenGL and sound effects via OpenAL. Supports 2 player Co-op and single player versus AI game play modes. It began as a simple project to implement a completely finished and working game utilizing modern C++. Since the completion of the working prototype, it has slowly become a test application for a growing set of common framework libraries.



### Rigel

![v3d](/uploads/2015/07/v3d-ss2_sm.png)

This is a GNU/Linux 3D Modelling Application. It supports a limited set of polygon objects (cube, cone, cylinder), standard transformation tools (rotate, translate, scale), interactive picking/selection of objects and sub-object components, and subobject component editing (edge/face/vertex transformations, face/edge splitting). It is built using GTK– for the interface and renders 3D scenes using OpenGL.


### libhookah

![code](/uploads/2015/07/code.jpg)


This is the common library used in pong, tetris, et al. It is written in modern C++ and utilizes features from the standard library and boost libraries. While it began as a single engine library, it is currently organized into a collection of small libraries. Each library provides a limited collection of services &#8211; config file parsing, abstract input device and event handling, concrete SDL binding, 3D data types, fonts, sound support. External dependencies include OpenAL for sound, SDL for video and input, and QuantumXML for config files.

### QuantumXML

An XML Parsing library with DOM API support written in C++.

### libluxa
An OpenGL GUI library.

