cmake_minimum_required(VERSION 3.20)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_GENERATOR_PLATFORM x64)

# ImGui
set(IMGUI_DIR "${CMAKE_CURRENT_SOURCE_DIR}")

file(GLOB IMGUI_HEADERS CONFIGURE_DEPENDS "${IMGUI_DIR}/*.h")
file(GLOB IMGUI_SOURCES CONFIGURE_DEPENDS "${IMGUI_DIR}/*.cpp")

add_library(imgui STATIC
        "${IMGUI_HEADERS}"
        "${IMGUI_SOURCES}"
        "${IMGUI_DIR}/backends/imgui_impl_dx12.cpp"
        "${IMGUI_DIR}/backends/imgui_impl_win32.cpp"
    )
    target_include_directories(imgui PUBLIC 
        "${IMGUI_DIR}" 
        "${IMGUI_DIR}/backends"
    )
target_link_libraries(imgui PRIVATE d3d12.lib dxgi.lib dxcompiler.lib DirectX-Headers)