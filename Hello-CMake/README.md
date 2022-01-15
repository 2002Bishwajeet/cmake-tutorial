# Hello CMake

In this first lesson we are gonna build a simple Hellow World program using CMake.

## Concepts

#### CMakeLists.txt

CMakeLists.txt is the file which should store all your CMake commands. When cmake is run in a folder it will look for this file and if it does not exist cmake will exit with an error.

#### Minimum CMake version

When creating a project using CMake, you can specify the minimum version of CMake that is supported.

`cmake_minimum_required(VERSION 3.0.0)`

#### Project

A CMake build can include a project name to make referencing certain variables easier when using multiple projects.

`project (hello_cmake)`

**NOTE:** A shorthand that some people use is to have the project name and executable name the same. This allows you to specify the CMakeLists.txt as follows,

```
cmake_minimum_required(VERSION 3.0)
project (hello_cmake)
add_executable(${PROJECT_NAME} hello.cpp)
```

#### Creating an Executable

The add_executable() command specifies that an executable should be build from the specified source files, in this example main.cpp. The first argument to the add_executable() function is the name of the executable to be built, and the second argument is the list of source files to compile.

`add_executable(hello_cmake main.cpp)`

#### Binary Directory

The root or top level folder that you run the cmake command from is known as your `CMAKE_BINARY_DIR` and is the root folder for all your binary files. CMake supports building and generating your binary files both in-place and also out-of-source.

##### In-Place Build

In-place builds generate all temporary build files in the same directory structure as the source code. This means that all Makefiles and object files are interspersed with your normal code. To create an in-place build target run the cmake command in your root directory. For example:

```bash
cmakeTut/Hello-CMake$ cmake .
-- The C compiler identification is GNU 9.3.0
-- The CXX compiler identification is GNU 9.3.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: /home/bishw/cppWorks/cmakeTut/Hello-CMake

cmakeTut/Hello-CMake$  tree
.
├── CMakeCache.txt
├── CMakeFiles
│   ├── 3.16.3
│   │   ├── CMakeCCompiler.cmake
│   │   ├── CMakeCXXCompiler.cmake
│   │   ├── CMakeDetermineCompilerABI_C.bin
│   │   ├── CMakeDetermineCompilerABI_CXX.bin
│   │   ├── CMakeSystem.cmake
│   │   ├── CompilerIdC
│   │   │   ├── CMakeCCompilerId.c
│   │   │   ├── a.out
│   │   │   └── tmp
│   │   └── CompilerIdCXX
│   │       ├── CMakeCXXCompilerId.cpp
│   │       ├── a.out
│   │       └── tmp
│   ├── CMakeDirectoryInformation.cmake
│   ├── CMakeOutput.log
│   ├── CMakeTmp
│   ├── Makefile.cmake
│   ├── Makefile2
│   ├── TargetDirectories.txt
│   ├── cmake.check_cache
│   ├── hello_cmake.dir
│   │   ├── DependInfo.cmake
│   │   ├── build.make
│   │   ├── cmake_clean.cmake
│   │   ├── depend.make
│   │   ├── flags.make
│   │   ├── link.txt
│   │   └── progress.make
│   └── progress.marks
├── CMakeLists.txt
├── Makefile
├── README.md
├── cmake_install.cmake
└── hello.cpp
```

##### Out-of-Source Build

Out-of-source builds allow you to create a single build folder that can be anywhere on your file system. All temporary build and object files are located in this directory keeping your source tree clean. To create an out-of-source build run the cmake command in the build folder and point it to the directory with your root `CMakeLists.txt` file. Using out-of-source builds if you want to recreate your cmake environment from scratch, you only need to delete your build directory and then rerun cmake.

For Example:

```bash
cmakeTut/Hello-CMake$ mkdir build
cmakeTut/Hello-CMake$ cd build/
-- The C compiler identification is GNU 9.3.0
-- The CXX compiler identification is GNU 9.3.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: /home/bishw/cppWorks/cmakeTut/Hello-CMake/build

cmakeTut/Hello-CMake/build$ cd ..

cmakeTut/Hello-CMake$ tree
.
├── CMakeCache.txt
├── CMakeFiles
│   ├── 3.16.3
│   │   ├── CMakeCCompiler.cmake
│   │   ├── CMakeCXXCompiler.cmake
│   │   ├── CMakeDetermineCompilerABI_C.bin
│   │   ├── CMakeDetermineCompilerABI_CXX.bin
│   │   ├── CMakeSystem.cmake
│   │   ├── CompilerIdC
│   │   │   ├── CMakeCCompilerId.c
│   │   │   ├── a.out
│   │   │   └── tmp
│   │   └── CompilerIdCXX
│   │       ├── CMakeCXXCompilerId.cpp
│   │       ├── a.out
│   │       └── tmp
│   ├── CMakeDirectoryInformation.cmake
│   ├── CMakeOutput.log
│   ├── CMakeTmp
│   ├── Makefile.cmake
│   ├── Makefile2
│   ├── TargetDirectories.txt
│   ├── cmake.check_cache
│   ├── hello_cmake.dir
│   │   ├── DependInfo.cmake
│   │   ├── build.make
│   │   ├── cmake_clean.cmake
│   │   ├── depend.make
│   │   ├── flags.make
│   │   ├── link.txt
│   │   └── progress.make
│   └── progress.marks
├── CMakeLists.txt
├── Makefile
├── README.md
├── build
├── cmake_install.cmake
└── hello.cpp
```

## Building the Hello Cmake Project

Below is sample output from building this example.

```bash
cmakeTut/Hello-CMake$ mkdir build
cmakeTut/Hello-CMake$ cd build/
cmakeTut/Hello-CMake/build$ cmake ..
-- The C compiler identification is GNU 9.3.0
-- The CXX compiler identification is GNU 9.3.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: /home/bishw/cppWorks/cmakeTut/Hello-CMake/build

$ make
Scanning dependencies of target hello_cmake
[ 50%] Building CXX object CMakeFiles/hello_cmake.dir/hello.cpp.o
[100%] Linking CXX executable hello_cmake
[100%] Built target hello_cmake

$ ./hello_cmake
Hello Cmake!
```

And voila thats the first step of building your first Cmake Project
