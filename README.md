# OpenGLTutorial
This is a tutorial of learning how to use OpenGL for CMPSC458 computer graphics course.
## What is OpenGL?
OpenGL(Open Graphic Library) is a software interface to graphics hardware.
It is a low-level graphics API to specify objects and operations for 3D graphics, which is independent to OS/hardware.
## How to get started?
Clone or download the code to your work directory, `$home = path/to/files`
### On Windows
1. Prerequest: 
    - cmake-gui >= 3.15.3
    - visual studio: 19 or higher
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
After you successfuly compile the project following our instruction, the **OpenGL_tutorial_I** part will show how to open a new window, display a triangle and has a basic *game loop*. A *game loop* is the while loop which contains the code which runs between every frame.

So now let's go deeper to the code and see what each functional part works.
### Initialization
In the main function, we firstly initialize and configure **glfw**.
**glfw** is a lightweight utility library for OpenGL. It implements simple windowing API for OpenGL, and provide callback driven event processing of display, keyboard, mouse, controllers, etc.
``
glfwInit();
``
This initial function is called for every OpenGL program.

### Create the window
We then create the window by using `glfwCreateWindow` function like this: 
``GLFWwindow* window = glfwCreateWindow(SCR_WIDTH, SCR_HEIGHT, "OpenGL Session I", NULL, NULL);``
The parameters of ``glfwCreateWindow`` are: width, height, window name, monitor (nullptr usually) and share (nullptr usually).

### Build and compile the shader
We will not cover much this part so far. We will go back to discuss more about vertex and fragment shader in the third Ray Tracing project. 
What you need to know now is that at least vertex and fragment shaders are required to set up if we want to do some rendering, and shader is written in the shader language GLSL (OpenGL Shading Language).
Here we only compile very simple vertex and fragment shaders.
- Vertex shader
```
#version 330 core
layout (location = 0) in vec3 aPos;

void main()
{
    gl_Position = vec4(aPos.x, aPos.y, aPos.z, 1.0);
}
```
- Fragment Shader
```
#version 330 core
out vec4 FragColor;

void main()
{
    FragColor = vec4(1.0f, 0.5f, 0.2f, 1.0f);
} 
```

### Vertex Input
The pipeline of rendering on an OpenGL/GLFW program is shown below.

1. Vertex data

    We firstly define the vertex data. As a tutorial example, we define 3 vertices of a triangle in a float-type array:
    ```
    float vertices[] = {
        -0.5f, -0.5f, 0.0f, // left  
        0.5f, -0.5f, 0.0f, // right 
        0.0f,  0.5f, 0.0f  // top   
    };
    ```
    Every three elements in this array indicates the ``x,y,z`` coordinate of a vertex.

2. Creating Vertex Buffer Object

    **VBO** (Vertex Buffer Object) sets up a buffer to send data to the GPU.
    The *VBO* is created by setting an unsigned int value to refer to it later:
    ```
    unsigned int VBO; \\Vertex Buffer Object ID
    glGenBuffers(1, &VBO); \\Generate Buffer
    ```
    We then bind the buffer with **VBO** and buffer the data to **VBO**:
    ```
    glBindBuffer(GL_ARRAY_BUFFER, VBO); \\Bind Buffer with VBO
    glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW); \\Send data to the buffer
    ```
    Here ``GL_ARRAY_BUFFER`` indicates the data type, and ``GL_STATIC_DRAW`` indicates how the GPU will treat the data. These two parameters will remain unchanged.

3. Creating Vertex Array Object

    Once we have the buffer, we need to tell OpenGL how to interpret the buffer.
    Similar to **VBO** initialization:
    ```
    unsigned int VAO; \\Vertex Array Object ID
    glGenVertexArrays(1, &VAO); \\Generate Vertex Array
    ```
    We then bind the vertex array:
    ```
    glBindVertexArray(VAO);
    ```
    **VAO** (Vertex Array Object) creates “attributes points” which tell OpenGL how to parse the data.
    ```
    glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 3 * sizeof(float), (void*)0);
    ```
    The parameters of ``glVertexAttribPointer`` are:
    - Location
    - Number of Components
    - Type
    - Normalize Data
    - Stride to next element in array
    - Starting Position of element

    Hence, here `3` indicates that each vertex is composed of 3 float type values. `3 * sizeof(float)`  indicates the stride to next vertex is the size of each vertex element, since the vertices are stored in a list. 

### Game Loop
The game loop is where we run the application.
1. Set background color
    
    - We set the background color by:
    ``glClearColor(0.2f, 0.3f, 0.3f, 1.0f);``
    , which specifies the red, green, blue, and alpha values.
    
    - Then clear any previous data in buffer:
    ``glClear(GL_COLOR_BUFFER_BIT);``

2. Draw our first triangle

    - We need to define how to render:
    ``glUseProgram(shaderProgram);``
    , which we will skip now and learn in next session.
    
    - Tell which data to use:
    ``glBindVertexArray(VAO);``
    
    - Draw object:
    ``glDrawArrays(GL_TRIANGLES, 0, 3);``
    , in which the parameters are:
        - Mode: Specifies what kind of primitives to render.
        - Starting index
        - Number of indices to be rendered
        
    In this example, `GL_TRIANGLES` tells the function to draw lines between every three points. It starts from the beginning of VAO and renders 3 vertices.
    Although `GL_TRIANGLES` is the easiest and most commonly used, there are other kinds of primitives, including points, lines, polygons, etc.

3. Check and call events and swap the buffers
    ```
    glfwSwapBuffers(window);
    glfwPollEvents();
    ```
    These two functions are called at the end of each loop, to swap the buffer and see if any keys were pressed since the last loop.

## Practice
Till now hope you have learnt the basic struture of an OpenGL program, and got familiar with these basic variables and functions.
As a practice, could you:
- Create a Second Triangle. You need to add more vertices, and change ``glDrawArrays`` to load 6 (instead of 3) vertices
- Create a rectangle by combining the two triangles.
- Change the color of the triangles.

## Acknowledgement
Thanks  to <learnopengl.com> for providing figures and some tutorials about how to draw a triangle.
Thanks to <https://github.com/Polytonic/Glitter/tree/master/Glitterwhich> for providing the shell for the tutorial code.
