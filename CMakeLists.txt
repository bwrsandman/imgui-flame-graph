cmake_minimum_required(VERSION 3.14 FATAL_ERROR)
cmake_policy(SET CMP0076 NEW)

project(imgui-flame-graph VERSION 1.02)

option(IMGUI_FLAME_GRAPH_BUILD_EXAMPLE "Build an example using flame graph." ON)

list(APPEND IMGUI_FLAME_GRAPH_DIRECTORIES ${CMAKE_CURRENT_SOURCE_DIR})

add_library(${PROJECT_NAME} INTERFACE)
target_sources(${PROJECT_NAME} INTERFACE
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/imgui_widget_flamegraph.cpp>
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/imgui_widget_flamegraph.h>)
target_include_directories(${PROJECT_NAME} INTERFACE $<BUILD_INTERFACE:${IMGUI_FLAME_GRAPH_DIRECTORIES}>)
target_compile_definitions(${PROJECT_NAME} INTERFACE IMGUI_DEFINE_MATH_OPERATORS)

if(IMGUI_FLAME_GRAPH_BUILD_EXAMPLE)
    add_subdirectory(example/)
endif()
