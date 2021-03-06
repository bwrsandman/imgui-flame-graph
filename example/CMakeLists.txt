if(${CMAKE_VERSION} VERSION_LESS 3.14)
    include(${CMAKE_CURRENT_SOURCE_DIR}/cmake/FetchContent.cmake)
else()
    include(FetchContent)
endif()

FetchContent_Declare(
    imgui
    GIT_REPOSITORY https://github.com/ocornut/imgui.git
    GIT_TAG master
)
FetchContent_MakeAvailable(imgui)

FetchContent_Declare(
  SDL2
  URL https://www.libsdl.org/release/SDL2-2.0.10.tar.gz
  URL_HASH MD5=5a2114f2a6f348bdab5bf52b994811db
)
FetchContent_MakeAvailable(SDL2)

FetchContent_Declare(
    gl3w
    GIT_REPOSITORY https://github.com/skaslev/gl3w.git
    GIT_TAG master
)
FetchContent_MakeAvailable(gl3w)

file(GLOB IMGUI_SOURCE
    ${imgui_SOURCE_DIR}/*.cpp
    ${imgui_SOURCE_DIR}/examples/imgui_impl_sdl.cpp
    ${imgui_SOURCE_DIR}/examples/imgui_impl_opengl3.cpp
)
add_executable(imgui-flame-graph-example main.cpp ${IMGUI_SOURCE})
target_include_directories(imgui-flame-graph-example PRIVATE ${imgui_SOURCE_DIR} ${imgui_SOURCE_DIR}/examples)
target_link_libraries(imgui-flame-graph-example PRIVATE SDL2 gl3w imgui-flame-graph)
target_compile_definitions(imgui-flame-graph-example PRIVATE IMGUI_IMPL_OPENGL_LOADER_GL3W)
