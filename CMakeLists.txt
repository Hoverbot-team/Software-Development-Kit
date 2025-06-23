cmake_minimum_required(VERSION 3.10)
project(HoverbotSDK)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Define a reusable SDK interface target with include path
add_library(SDKInterface INTERFACE)
target_include_directories(SDKInterface INTERFACE ${CMAKE_SOURCE_DIR}/SDKInclude)

# Automatically add each plugin subdirectory if it has a CMakeLists.txt
file(GLOB children RELATIVE ${CMAKE_SOURCE_DIR}/Plugins ${CMAKE_SOURCE_DIR}/Plugins/*)

foreach(child ${children})
    message(STATUS "Found plugin candidate: ${child}")
    if(IS_DIRECTORY ${CMAKE_SOURCE_DIR}/Plugins/${child})
        if(EXISTS ${CMAKE_SOURCE_DIR}/Plugins/${child}/CMakeLists.txt)
            message(STATUS "Adding plugin: ${child}")
            add_subdirectory(Plugins/${child})
        endif()
    endif()
endforeach()
