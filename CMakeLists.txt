cmake_minimum_required(VERSION 3.12)

project(switch VERSION 0.0.1 DESCRIPTION "switch")


set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

find_package(USD REQUIRED)
find_package(Python COMPONENTS Interpreter Development REQUIRED)

include(GNUInstallDirs)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
add_definitions(-DGLEW_STATIC)

add_subdirectory(vendors)

add_executable(switch main.cpp scene.cpp)
target_include_directories(switch
    PUBLIC
        ${USD_INCLUDE_DIR}
        ${Python_INCLUDE_DIRS}
)
target_link_libraries(switch
    PUBLIC
        ${USD_BOOST_LIBRARIES}
        ${USD_LIBRARIES}
        ${Python_LIBRARIES}
        libglew_static
        glfw
)
