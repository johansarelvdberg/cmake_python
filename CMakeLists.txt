cmake_minimum_required(VERSION 3.9)
project(python_managed) 
set(CMAKE_CXX_STANDARD 17) # Set our source files as just the main.cpp
set(SOURCE_FILES main.cpp) # Create our executable file from our source files
#add_executable(gen_data ${SOURCE_FILES}) 
include(CMakeDependentOption)
add_subdirectory(packages)

# https://gitlab.kitware.com/cmake/community/-/wikis/FAQ#how-do-i-use-cmake-to-build-latex-documents
# https://cmake.org/cmake/help/latest/command/add_custom_command.html


 