cmake_minimum_required(VERSION 3.5)

project(WalnutApp)

set(CMAKE_CXX_STANDARD 17)

find_package(Vulkan REQUIRED)
find_package(glfw3 REQUIRED)
find_package(glm REQUIRED)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/Walnut/src)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/WalnutApp/src)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/vendor/imgui)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/vendor/stb_image)

file(GLOB IMGUI_FILES 
        vendor/imgui/*.h vendor/imgui/*.cpp 
        vendor/imgui/backends/backends/imgui_impl_vulkan.h vendor/imgui/backends/backends/imgui_impl_vulkan.cpp
        vendor/imgui/backends/backends/imgui_impl_glfw.h vendor/imgui/backends/backends/imgui_impl_glfw.cpp
)
file(GLOB STB_IMAGE_FILES vendor/stb_image/stb_image.h)
file(GLOB WALNUT_FILES 
        Walnut/src/Walnut/*.h Walnut/src/Walnut/*.cpp
        Walnut/src/Walnut/ImGui/*.h Walnut/src/Walnut/ImGui/*.cpp
        Walnut/src/Walnut/Input/*.h Walnut/src/Walnut/Input/*.cpp
    )

# Add main source file as executable
add_executable(WalnutApp WalnutApp/src/WalnutApp.cpp ${IMGUI_FILES} ${STB_IMAGE_FILES} ${WALNUT_FILES})
target_link_libraries(WalnutApp glfw ${Vulkan_LIBRARIES})  # Link with the submodules (GLFW, imgui)