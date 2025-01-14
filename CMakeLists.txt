cmake_minimum_required(VERSION 3.10)

# Set the project name and specify the C++ standard
project(OpenGLProject)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Set compilers (Clang)
set(CMAKE_C_COMPILER clang)
set(CMAKE_CXX_COMPILER clang++)

# Set build type
set(CMAKE_BUILD_TYPE Debug)

# Set source files
set(SOURCES
    src/main.cpp
)

# Create the executable
add_executable(OpenGLProject ${SOURCES})

# Enable Clang-Tidy for static analysis
set(CMAKE_CXX_CLANG_TIDY "clang-tidy;-checks=*")

# Enable all warnings and treat them as errors
target_compile_options(OpenGLProject PRIVATE 
    -Wall
    -Wextra
    -pedantic
    -Werror
)

# Enable clang-format on save or as part of the build process
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Enforce the use of modern C++ features (C++20)
target_compile_features(OpenGLProject PRIVATE cxx_std_20)

