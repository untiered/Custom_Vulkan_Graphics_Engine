cmake_minimum_required (VERSION 3.29)
project(HelloWorld LANGUAGES CXX)

# Use C++20 standard
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Make CMake aware of project-specific Find*.cmake files
# (optional, only needed if using custom FindVulkan.cmake)
list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/CMake")

# Find Vulkan
find_package(Vulkan REQUIRED)

# Find other dependencies installed via vcpkg
find_package(glfw3 CONFIG REQUIRED)
find_package(glm CONFIG REQUIRED)
find_package(tinyobjloader CONFIG REQUIRED)

# Add your executable
add_executable(HelloWorld
    ${CMAKE_CURRENT_SOURCE_DIR}/../HelloWorld.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/../Source/Graphics/VKInstanceLimb.cpp
)

# Include all relevant headers
target_include_directories(HelloWorld
    PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/../Includes
)

# Link all dependencies
target_link_libraries(HelloWorld
    PRIVATE
        Vulkan::Vulkan   # Traditional Vulkan headers
        glfw
        glm::glm
        tinyobjloader::tinyobjloader
)

