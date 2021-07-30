cmake_minimum_required(VERSION 3.19)
project(OGLTemplate)

find_package(assimp CONFIG REQUIRED)
find_path(STB_INCLUDE_DIRS "stb.h")
find_package(freetype CONFIG REQUIRED)
find_package(GLEW REQUIRED)
find_package(glfw3 CONFIG REQUIRED)
find_package(glm CONFIG REQUIRED)
find_package(imgui CONFIG REQUIRED)
find_package(glad CONFIG REQUIRED)
set(CMAKE_EXPORT_COMPILE_COMMANDS on)

set(CMAKE_CXX_STANDARD 20)
file(GLOB SOURCE
        "src/*.h"
        "src/*.hpp"
        "src/*.cpp"
        "src/*.gs"
        "src/*.vs"
        "src/*.fs"
        )

configure_file(${CMAKE_SOURCE_DIR}/configure/root_directory.h.in ${CMAKE_SOURCE_DIR}/configure/root_directory.h)
include_directories(${CMAKE_SOURCE_DIR}/configure)
#message(${CMAKE_SOURCE_DIR})

add_executable(OGLTemplate ${SOURCE})

include_directories(${CMAKE_SOURCE_DIR}/includes)
target_link_libraries(OGLTemplate PRIVATE glad::glad)
target_include_directories(OGLTemplate PRIVATE ${STB_INCLUDE_DIRS})
target_link_libraries(OGLTemplate PRIVATE assimp::assimp)
target_link_libraries(OGLTemplate PRIVATE freetype)
target_link_libraries(OGLTemplate PRIVATE GLEW::GLEW)
target_link_libraries(OGLTemplate PRIVATE glfw)
target_link_libraries(OGLTemplate PRIVATE glm::glm)
target_link_libraries(OGLTemplate PRIVATE imgui::imgui)