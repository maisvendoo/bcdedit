# CMake required version
cmake_minimum_required (VERSION 3.4)

# Project name
set (PROJECT bcdedit)

# Find all sources
aux_source_directory("src" SRC)

include_directories("include")

# Binary dir is one level upper that build directory
set (BINARY_DIR ../)

# Set flags and output directories for different configurations
if ( CMAKE_BUILD_TYPE STREQUAL "DEBUG" )

    add_definitions( -DAPP_DEBUG )
    set (EXECUTABLE_OUTPUT_PATH ${BINARY_DIR}/bin/Debug/)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wall -g")

else()

    set (EXECUTABLE_OUTPUT_PATH ${BINARY_DIR}/bin/Release/)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wall -O2")

endif()

# Add aux libs
set (LIBS uuid hivex)

# Build executable
add_executable (${PROJECT} ${SRC})

# Link executable with libs
target_link_libraries(${PROJECT} ${LIBS})