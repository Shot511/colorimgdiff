# Copyright (C) 2020 Tomasz Gałaj

cmake_minimum_required(VERSION 3.9.2 FATAL_ERROR)
project(colorimgdiff VERSION 0.1)

# add thirdparties
set(STB_IMAGE_LIBRARY "stb_image")
add_library(${STB_IMAGE_LIBRARY} STATIC include/stb_image.cpp include/stb_image_write.cpp)
target_include_directories(${STB_IMAGE_LIBRARY} PRIVATE include)

# Add source files
file(GLOB SOURCE_FILES_EXE 
	 ${CMAKE_CURRENT_SOURCE_DIR}/*.c
	 ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)

# Add header files
file(GLOB HEADER_FILES_EXE 
	 ${CMAKE_CURRENT_SOURCE_DIR}/*.h
	 ${CMAKE_CURRENT_SOURCE_DIR}/*.hpp)

# Define the executable
add_executable(${PROJECT_NAME} ${HEADER_FILES_EXE} ${SOURCE_FILES_EXE})
set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD 17)

# Define the include DIRs
target_include_directories(${PROJECT_NAME} PRIVATE include)

# Define the link libraries
target_link_libraries(${PROJECT_NAME} ${STB_IMAGE_LIBRARY})

source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR} PREFIX "sources" FILES ${SOURCE_FILES_EXE})						   
source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR} PREFIX "headers" FILES ${HEADER_FILES_EXE})