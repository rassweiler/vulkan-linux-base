cmake_minimum_required (VERSION 3.20)
project (VulkanTest)

set(CMAKE_CXX_STANDARD 20)

if(CMAKE_SYSTEM_NAME STREQUAL "Linux")
message(STATUS "Linux Seup")

#find_path(VULKAN_INCLUDE_DIR NAMES vulkan/vulkan.h HINTS
#            "$ENV{VULKAN_SDK}/include")
#find_library(VULKAN_LIBRARY NAMES vulkan HINTS
#            "$ENV{VULKAN_SDK}/lib")

find_package(Vulkan REQUIRED)
find_package(OpenGL REQUIRED)
find_package(glfw3 REQUIRED)
find_package(GLEW REQUIRED)
find_package(X11 REQUIRED)

endif()

include_directories(
	${Vulkan_INCLUDE_DIRS}
	${OPENGL_INCLUDE_DIRS} 
   ${GLFW_INCLUDE_DIRS}
   ${GLEW_INCLUDE_DIRS}
	${X11_INCLUDE_DIR}
   ${PROJECT_SOURCE_DIR}
)

#list(APPEND LIBS ${VULKAN_LIBRARY})

set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Werror -std=c++20 -O2")
#set (CMAKE_CXX_IMPLICIT_LINK_LIBRARIES "${CMAKE_CXX_IMPLICIT_LINK_LIBRARIES} -lglfw -lvulkan -ldl -lpthread -lX11 -lXxf86vm -lXrandr -lXi")
set (source_dir "${PROJECT_SOURCE_DIR}/src/")
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/build)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/build)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

file (GLOB source_files "${source_dir}/*.cpp")

add_executable (VulkanTest ${source_files})

#target_link_libraries(VulkanTest ${VULKAN_LIBRARY} glfw ${X11_LIBRARIES} Xi Xxf86vm pthread dl)
target_link_libraries(VulkanTest glfw vulkan dl pthread X11 Xxf86vm Xrandr Xi)