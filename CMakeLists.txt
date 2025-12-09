cmake_minimum_required(VERSION 3.12)

project(libfmt
    VERSION 1.0.0
    LANGUAGES CXX
)

# Set C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Platform detection
if(WIN32)
    set(PLATFORM_NAME "win32")
elseif(APPLE)
    set(PLATFORM_NAME "macos")
else()
    set(PLATFORM_NAME "linux")
endif()

# Output directories
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/bin/${PLATFORM_NAME})

# Collect source files
file(GLOB FMT_SOURCES
    ${CMAKE_CURRENT_SOURCE_DIR}/src/*.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/src/*.c
)

# Create static library
add_library(fmt STATIC ${FMT_SOURCES})

# Include directories
target_include_directories(fmt
    PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/include
)

# Compiler flags
if(NOT MSVC)
    target_compile_options(fmt PRIVATE -Wall -Wno-unused-value -Wno-unused-but-set-variable -fPIC)
endif()
