# OpenGLTutorial
This is a tutorial of learning how to use OpenGL for CMPSC458 computer graphic course.
## What is OpenGL?
OpenGL(Open Graphic Library) is a software interface to graphics hardware.
It is a low-level graphics API to specify objects and operations for 3D graphics, which is independent to OS/hardware.
## How to get started?
Clone or download the code to your work directory, **home = path/to/files**
### On Windows
1. Prerequest: 
  - cmake-gui >= 3.15.3
  - visual studio: 19 or higher
2. Configure the project:
  - Create a build directory *Build* under **home**.
  - Open cmake-gui (already installed on lab machines or install it on your personal computer if you are using that).
  - Set source code to: **home**
  - Set build the binaries to: **home/Build**
  - Press Configure and specify the generator to proper visual studio in your system (no need to change by default).
  - Press Configure twice or more, until no more red entrie.
  - Press Generate
3. Run the project on Visual Studio:
  - Press 
### On Linux/Mac 
1. Prerequest:
  - cmake >= 3.15.3
2. Configure the project:
  - `cd` into **home**.
  - `mkdir Build`
  - `cd Build`
  - Run `make -j4` takes some time, replace the 4 with the number of cores on you machine.
  - 
