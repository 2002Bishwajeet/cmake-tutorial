cmake_minimum_required(VERSION 3.0.0)


project(static_lib)

############################################################
# Create a library
############################################################

# Generate the static library from the library sources
add_library(${PROJECT_NAME} STATIC
    src/hello.cpp
)

target_include_directories(${PROJECT_NAME} PUBLIC
    ${PROJECT_SOURCE_DIR}/include
)



############################################################
# Create an executable
############################################################


# Add an executable with the above sources
add_executable(hello_binary # hello_binary is the executable name
    src/main.cpp
)


#  Time to link the new [PROJECT_NAME] target with the hello_binary target

target_link_libraries(hello_binary PRIVATE
    ${PROJECT_NAME} #Linking [PROJECT_NAME] with hello_binary
)

