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

# Locate clang-format executable
find_program(CLANG_FORMAT_EXECUTABLE clang-format)

# Check if clang-format exists
if (CLANG_FORMAT_EXECUTABLE)
  # Collect all .cpp and .h files
  file(GLOB ALL_SOURCE_FILES
    ${CMAKE_SOURCE_DIR}/src/*.cpp
    ${CMAKE_SOURCE_DIR}/include/*.h
  )

  add_custom_command(
    TARGET OpenGLProject PRE_BUILD
    COMMAND ${CLANG_FORMAT_EXECUTABLE} -i ${ALL_SOURCE_FILES}
    COMMENT "Running clang-format before build"
  )
else()
  message(FATAL_ERROR "clang-format executable not found!")
endif()

