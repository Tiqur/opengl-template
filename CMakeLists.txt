cmake_minimum_required(VERSION 3.10)

# Specify the C++ standard
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Set to build type
set(CMAKE_BUILD_TYPE Debug)

# Set the project name
project(OpenGLProject)

# Set source files
set(SOURCES
    src/main.cpp
)

# Create the executable
add_executable(OpenGLProject ${SOURCES})

# Enable all warnings + treat warning as errors
target_compile_options(OpenGLProject PRIVATE -Wall -Wextra -pedantic -Werror)

