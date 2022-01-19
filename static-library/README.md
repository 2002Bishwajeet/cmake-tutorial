## Static Library

This tutorial shows how to run a basic hello world program and links to a static library.

## Introduction

Files in the tutorial include

```bash
$ tree
.
├── CMakeLists.txt
├── README.md
├── include
│ └── static
│ └── hello.h
└── src
├── hello.cpp
└── main.cpp
```

- [CMakeLists.txt](static-library/CMakeLists.txt) - Contains the CMake commands you wish to run

- [include/static/hello.h](static-library/include/static/hello.h) - The header file to include

- [src/hello.cpp](static-library/src/hello.cpp) - A source file to compile

- [src/main.cpp](static-library/src/main.cpp) - The source file with main

## Concepts

### Adding a Static Library

The `add_library()` function is used to create a library from some source files. This is called as follows:

```CMake
add_library(hello STATIC src/hello.cpp)
```

This will be used to create a static library with the name `libhello.a` with the sources in the `add_library()` call.

**NOTE:** As mentioned in the previous example, we pass the source files directly to the add_library call, as recommended for modern CMake.

### Populating Including Directories

In this example, we include directories in the library using the `target_include_directories()` function with the scope set to **PUBLIC**.

```CMake

target_include_directories(${PROJECT_NAME}
    PUBLIC
        ${PROJECT_SOURCE_DIR}/include
)
```

This will cause the included directory used in the following places:

When compiling the library

When compiling any additional target that links the library.

The meaning of scopes are:

**PRIVATE** - the directory is added to this target’s include directories

**INTERFACE** - the directory is added to the include directories for any targets that link this library.

**PUBLIC** - As above, it is included in this library and also any targets that link this library.

**TIP:**

For public headers it is often a good idea to have your include folder be "namespaced" with sub-directories.

The directory passed to target_include_directories will be the root of your include directory tree and your C++ files should include the path from there to your header.

For this example you can see that we do it as follows:

`#include "static/Hello.h"`

Using this method means that there is less chance of header filename clashes when you use multiple libraries in your project.

## Linking a Library

When creating an executable that will use your library you must tell the compiler about the library. This can be done using the `target_link_libraries()` function.

```CMake
add_executable(hello_binary
    src/main.cpp
)

target_link_libraries( hello_binary
    PRIVATE
        hello_library
)
```
