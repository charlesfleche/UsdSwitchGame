cmake_minimum_required(VERSION 3.12)

project(switch VERSION 0.0.1 DESCRIPTION "switch")

include(${PXR_USD_LOCATION}/pxrConfig.cmake)

include(GNUInstallDirs)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

add_subdirectory(vendors)

file(GLOB SRC_CPP RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} "src/*.cpp")

add_executable(${PROJECT_NAME} ${SRC_CPP})
target_include_directories(${PROJECT_NAME}
    PUBLIC
    ${PXR_INCLUDE_DIRS}
)
target_link_libraries(${PROJECT_NAME}
    PUBLIC
    ${PXR_LIBRARIES}
    glfw
)

file(GLOB USDA_FILES RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} "resources/*.usda")

install(TARGETS ${PROJECT_NAME})
install(FILES ${USDA_FILES} DESTINATION ${CMAKE_INSTALL_BINDIR} )

