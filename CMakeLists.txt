cmake_minimum_required(VERSION 3.10 FATAL_ERROR)

project(imgui-flame-graph)

option(IMGUI_FLAME_GRAPH_BUILD_EXAMPLE "Build an example using flame graph." ON)

file(GLOB IMGUI_FLAME_GRAPH_SOURCE *.cpp *.h)
list(APPEND IMGUI_FLAME_GRAPH_DIRECTORIES ${CMAKE_CURRENT_SOURCE_DIR})

add_library(${PROJECT_NAME} INTERFACE)
target_sources(${PROJECT_NAME} INTERFACE $<BUILD_INTERFACE:${IMGUI_FLAME_GRAPH_SOURCE}>)
target_include_directories(${PROJECT_NAME} INTERFACE $<BUILD_INTERFACE:${IMGUI_FLAME_GRAPH_DIRECTORIES}>)

if(IMGUI_FLAME_GRAPH_BUILD_EXAMPLE)
    add_subdirectory(example/)
endif()
