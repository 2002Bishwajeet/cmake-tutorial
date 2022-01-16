## Hello Headers

This shows how to work with custom header files and your cpp files using CMake.

## Introduction

Files in the tutorial include

```bash
.
├── CMakeLists.txt
├── README.md
├── include
│   └── hello.h
└── src
    ├── hello.cpp
    └── main.cpp
```

- [CMakeLists.txt](Hello-headers/CMakeLists.txt) - Contains the CMake commands you wish to run.

- [include/hello.h](Hello-headers/include/hello.h) - The header file to include.

- [src/hello.cpp](Hello-headers/src/hello.cpp) - A source file to compile.

- [src/main.cpp](Hello-headers/src/main.cpp) - The source file with main.

## Concepts

### Directory Paths

CMake syntax specifies a number of variables which can be used to help find useful directories in your project or source tree. Some of these include:

|         Variable         |                                           Info                                            |
| :----------------------: | :---------------------------------------------------------------------------------------: |
|     CMAKE_SOURCE_DIR     |                                 The root source directory                                 |
| CMAKE_CURRENT_SOURCE_DIR |            The current source directory if using sub-projects and directories.            |
|    PROJECT_SOURCE_DIR    |                    The source directory of the current cmake project.                     |
|     CMAKE_BINARY_DIR     | The root binary / build directory. This is the directory where you ran the cmake command. |
| CMAKE_CURRENT_BINARY_DIR |                         The build directory you are currently in.                         |
|    PROJECT_BINARY_DIR    |                       The build directory for the current project.                        |

### Source Files Variable

Creating a variable which includes the source files allows you to be clearer about these files and easily add them to multiple commands, for example, the add_executable() function.

```bash
# Create a sources variable with a link to all cpp files to compile
set(SOURCES # This is a variable
    src/hello.cpp
    src/main.cpp
)
# In short, to create a variable in CMAKE, use the set() command.

add_executable(${PROJECT_NAME} ${SOURCES})
```

**NOTE:** An alternative to setting specific file names in the SOURCES variable is to use a `GLOB` command to find files using wildcard pattern matching.

`file(GLOB SOURCES "src/*.cpp")`

**TIP:** For modern CMake it is NOT recommended to use a variable for sources. Instead it is typical to directly declare the sources in the `add_xxx` function.
This is particularly important for glob commands which may not always show you the correct results if you add a new source file.

### Including Directories

When you have different include folders, you can make your compiler aware of them using the `target_include_directories()` function. When compiling this target this will add these directories to the compiler with the -I flag e.g. -I/directory/path

The PRIVATE identifier specifies the scope of the include. This is important for libraries and is explained in the next example. More details on the function is available [here](https://cmake.org/cmake/help/latest/command/target_include_directories.html)

**NOTE:** Remember to add `target_include_directories()` after the `add_executable()` function otherwise you will get this following error

```bash
CMake Error at CMakeLists.txt:19 (target_include_directories):
  Cannot specify include directories for target "hello_headers" which is not
  built by this project.
```


