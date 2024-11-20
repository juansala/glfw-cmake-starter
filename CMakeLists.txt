# This file contains a simple CMake source tree root configuration for 
# building an OpenGL-based application using GLFW (and GLAD).
# Note: To get title bars and borders working in WSL (Ubuntu 22.04), generate 
# the build files without the Wayland backend. For example, after making a build
# directory and navigating into it, use the following command:
# cmake .. -D GLFW_BUILD_WAYLAND=0

# Resources:
# - https://learnopengl.com (Redirected to GLFW site)
# - https://github.com/glfw (See issue #1489)
# - https://www.glfw.org/ (Compiling and building applications)
# - https://github.com/enkisoftware/GLFW-CMake-starter/tree/main

cmake_minimum_required(VERSION 3.5)

project(glfw_wsl_cmake_starter VERSION 1.0)

# specify the C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Add glfw source tree root directory
add_subdirectory(${CMAKE_SOURCE_DIR}/glfw)

# Add GLAD as a library
add_library(glad ${CMAKE_SOURCE_DIR}/glad/glad.c)
target_include_directories(glad PUBLIC ${CMAKE_SOURCE_DIR}/include)

# Add test script as executable
add_executable(glfw_window_example glfw_window_example.cpp)

# Add all the include directories
target_include_directories(glfw_window_example PUBLIC
                           ${GLFW_SOURCE_DIR}/deps)

# Link against the dependencies
target_link_libraries(glfw_window_example glfw glad)