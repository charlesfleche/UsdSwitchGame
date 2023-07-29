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

file(GLOB SRC_CPP RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} "src/*.cpp")

add_executable(${PROJECT_NAME} ${SRC_CPP})
target_include_directories(${PROJECT_NAME}
    PUBLIC
        ${USD_INCLUDE_DIR}
        ${Python_INCLUDE_DIRS}
)
target_link_libraries(${PROJECT_NAME}
    PUBLIC
        ${USD_BOOST_LIBRARIES}
        ${USD_LIBRARIES}
        ${Python_LIBRARIES}
        libglew_static
        glfw
)

file(GLOB USDA_FILES RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} "resources/*.usda")

install(TARGETS ${PROJECT_NAME})
install(FILES ${USDA_FILES} DESTINATION ${CMAKE_INSTALL_BINDIR} )

