# OpenGLTutorial
This is a tutorial of learning how to use OpenGL for CMPSC458 computer graphic course.
## What is OpenGL?
OpenGL(Open Graphic Library) is a software interface to graphics hardware.
It is a low-level graphics API to specify objects and operations for 3D graphics, which is independent to OS/hardware.
## How to get started?
Clone or download the code to your work directory, `$home = path/to/files`
### On Windows
1. Prerequest: 
  -- cmake-gui >= 3.15.3
  -- visual studio: 19 or higher
2. Configure the project:
  - Create a build directory `Build` under `$home`.
  - Open cmake-gui (already installed on lab machines or install it on your personal computer if you are using that).
  - Set source code to: `home`
  - Set build the binaries to: `home/Build`
  - Press Configure and specify the generator to proper visual studio in your system (no need to change by default).
  - Press Configure twice or more, until no more red entrie.
  - Press Generate
3. Run the project in Visual Studio:
  - In cmake-gui, press Open Project to run the project.
  - In VS, right click on Solution and select project **OpenGL_tutorial_I** for the single startup project.
  - In VS, build the project (you can just click on Local Windows Debugger and it will build it). This takes some time the first time but is much faster every other
time.
  
### On Linux/Mac 
1. Prerequest:
  - cmake >= 3.15.3
2. Configure the project:
  - `cd $home`.
  - `mkdir Build`
  - `cd Build`
  - Run `make -j4`. It takes some time, you may replace the 4 with the number of cores on you machine.
  - From the `$home/Build` directory, Run `./OpenGL_tutorial_I` to run the project. You can edit the source files with whatever editor you like though if you want to add
more files, you will have to run cmake again (which you can from the command line with `cmake ..` from the `Build` folder and the files will automatically be added if they are in the same locations as the starter code).

## How does the code work?
After you successfuly compile the project following our instruction, the **OpenGL_tutorial_I** part will show how to open a new window, display a triangle and has a basic [^gameloop].
[^gameloop]:A game loop is the while loop which contains the code which runs between every frame.
