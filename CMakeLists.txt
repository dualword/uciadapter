cmake_minimum_required(VERSION 3.10)
project(uciadapter)

# Configure Process
add_definitions(-DUNIX)
SET(process src/ProcessLinux.cpp)
if(WIN32)
    remove_definitions(-DUNIX)
    message(FATAL_ERROR "uciadapter is not yet compatible with Windows")
endif()
add_library(uciadapter SHARED src/UCI.cpp ${process})

# Includes
set(UCIADAPTER_INCLUDE_DIR ${CMAKE_CURRENT_BINARY_DIR}/includes) # For conveniance
set(UCIADAPTER_INCLUDE_DIR ${UCIADAPTER_INCLUDE_DIR} PARENT_SCOPE) # To be used by other projects with add_subdirectory()
file(MAKE_DIRECTORY ${UCIADAPTER_INCLUDE_DIR})
configure_file(src/UCI.hpp ${UCIADAPTER_INCLUDE_DIR} COPYONLY)
configure_file(src/Process.hpp ${UCIADAPTER_INCLUDE_DIR} COPYONLY)
configure_file(src/ProcessLinux.hpp ${UCIADAPTER_INCLUDE_DIR} COPYONLY)
include_directories(${UCIADAPTER_INCLUDE_DIR})

# Tests
enable_testing()
add_subdirectory("tests/")