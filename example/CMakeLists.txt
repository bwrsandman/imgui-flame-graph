include(FetchContent)

FetchContent_Declare(
    imgui
    GIT_REPOSITORY https://github.com/ocornut/imgui.git
    GIT_TAG master
)
FetchContent_MakeAvailable(imgui)

FetchContent_Declare(
  SDL2
  URL https://www.libsdl.org/release/SDL2-2.26.5.tar.gz
  URL_HASH MD5=47f22c109070431ecccd90abd3c0ab6e
)
FetchContent_MakeAvailable(SDL2)

FetchContent_Declare(
    gl3w
    GIT_REPOSITORY https://github.com/bwrsandman/gl3w.git
    GIT_TAG master
)
FetchContent_MakeAvailable(gl3w)

file(GLOB EXTERNAL_SOURCE
    ${imgui_SOURCE_DIR}/*.cpp
    ${imgui_SOURCE_DIR}/backends/imgui_impl_sdl2.cpp
    ${imgui_SOURCE_DIR}/backends/imgui_impl_opengl3.cpp
)
add_executable(imgui-flame-graph-example main.cpp ${EXTERNAL_SOURCE})
target_include_directories(imgui-flame-graph-example
    PRIVATE
        ${imgui_SOURCE_DIR}
        ${imgui_SOURCE_DIR}/backends
        ${imgui_SOURCE_DIR}/examples
        ${gl3w_BINARY_DIR}/include
)
target_link_libraries(imgui-flame-graph-example PRIVATE gl3w SDL2 imgui-flame-graph ${CMAKE_DL_LIBS})
target_compile_definitions(imgui-flame-graph-example PRIVATE IMGUI_IMPL_OPENGL_LOADER_GL3W)
target_compile_features(imgui-flame-graph-example PRIVATE cxx_constexpr)
