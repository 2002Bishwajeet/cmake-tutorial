# Set the minimum version of CMake that can be used
# To find the cmake version run
# $ cmake --version
# Minimum cmake version required 
cmake_minimum_required(VERSION 3.0)

# Set a Project name
# [project] must be lowercase
# A CMake build can include a project name to make referencing certain variables easier when using multiple projects.
project(hello_cmake)

#  [add_executable] command specifies that an executable should be build from the specified source files, in this example hello.cpp.
#  The first argument to the add_executable() function is the name of the executable to be built, 
#   and the second argument is the list of source files to compile.
add_executable(${PROJECT_NAME} hello.cpp) # here PROJECT_NAME is "hello_cmake"
# an executable file will be built in the name of [PROJECT_NAME]
#  If you want the executable to be named differently, you can replace ${PROJECT_NAME} with the name you want.


