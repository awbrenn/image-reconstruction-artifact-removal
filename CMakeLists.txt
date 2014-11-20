cmake_minimum_required(VERSION 2.8.4)
project(lab07)

set(SOURCE_FILES warp.cpp)

if(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
    include_directories("/usr/local/include")
    find_library(OIIO "OpenImageIO" "/usr/local/lib")
    find_library(FOUNDATION "Foundation")
    find_library(GLUT "GLUT")
    find_library(OPENGL "OpenGL")
elseif(${CMAKE_SYSTEM_NAME} MATCHES "Linux")
    include_directories("/group/dpa/include")
    find_library(OIIO "OpenImageIO" "/group/dpa/lib")
    find_library(GLUT "glut")
    find_library(GL "GL")
    find_library(GLU "GLU")
endif(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")

add_executable(warp ${SOURCE_FILES})

if(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
    target_link_libraries(warp ${OIIO} ${FOUNDATION} ${GLUT} ${OPENGL})
elseif(${CMAKE_SYSTEM_NAME} MATCHES "Linux")
    target_link_libraries(warp ${OIIO} ${GLUT} ${GL} ${GLU})
endif(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")

