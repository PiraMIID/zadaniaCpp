cmake_minimum_required(VERSION 3.17)
project(zadaniaCpp )

#set(CMAKE_CXX_STANDARD 11)
set(CMAKE_BUILD_TYPE Debug)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -O0 -Wno-unused-variable")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -O0 -Wno-unused-variable -Wliteral-conversion")


#----------------------------------------------------------------------
include(CheckCXXCompilerFlag)
CHECK_CXX_COMPILER_FLAG("-std=c++11" COMPILER_SUPPORTS_CXX11)
CHECK_CXX_COMPILER_FLAG("-std=c++0x" COMPILER_SUPPORTS_CXX0X)
if(COMPILER_SUPPORTS_CXX11)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
elseif(COMPILER_SUPPORTS_CXX0X)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")
else()
    message(STATUS "The compiler ${CMAKE_CXX_COMPILER} has no C++11 support. Please use a different C++ compiler.")
endif()

file(GLOB_RECURSE APP_SOURCES */*.cc)


foreach (sourcefile ${APP_SOURCES})
    #get filename without extension (NAME_(W)ethout(E)xtenction)
    get_filename_component(filename ${sourcefile} NAME_WE)
    #add executable for all file
    add_executable(${filename} ${sourcefile})
endforeach (sourcefile ${APP_SOURCES})