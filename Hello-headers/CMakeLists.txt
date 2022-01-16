# Set the minimum version of CMake that can be used
# To find the cmake version run
# $ cmake --version
# Minimum cmake version required 
cmake_minimum_required(VERSION 3.0.0)

# Set the Project Name
project(hello_headers)

#  To create a Variable in CMake, use the set() method for it
set(SOURCES
    src/hello.cpp
    src/main.cpp
)

#  [add_executable] command specifies that an executable should be build from the specified source files, in this example hello.cpp.
#  The first argument to the add_executable() function is the name of the executable to be built, 
#   and the second argument is the list of source files to compile.
add_executable(${PROJECT_NAME} ${SOURCES}) # here PROJECT_NAME is "hello_cmake"
# an executable file will be built in the name of [PROJECT_NAME]
#  If you want the executable to be named differently, you can replace ${PROJECT_NAME} with the name you want.

#  Remember that [target_include_directories()] must be used after [add_executable()] to specify the directories that should be added to the include path.

# Set the directories that should be included in the build command for this target
# when running g++ these will be included as -I/directory/path/
target_include_directories(${PROJECT_NAME} 
    PRIVATE
        ${PROJECT_SOURCE_DIR}/include #About [PROJECT_SOURCE_DIR] in README
)
