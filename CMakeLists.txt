cmake_minimum_required(VERSION 3.15)
project(PortalCube VERSION 1.0 LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

file(GLOB SRC_FILES ${CMAKE_SOURCE_DIR}/src/*.cpp)

add_library(glad STATIC ${CMAKE_SOURCE_DIR}/libs/glad.c)

target_include_directories(glad PUBLIC ${CMAKE_SOURCE_DIR}/libs/include)

add_executable(PortalCube
    ${CMAKE_SOURCE_DIR}/main.cpp
    ${SRC_FILES}
)

target_include_directories(PortalCube PRIVATE
    ${CMAKE_SOURCE_DIR}/include
    ${CMAKE_SOURCE_DIR}/libs/include
)

link_directories(${CMAKE_SOURCE_DIR}/libs/lib)

target_link_libraries(PortalCube
    glad
    ${CMAKE_SOURCE_DIR}/libs/lib/libglfw3.a
    opengl32
    gdi32
)

get_target_property(library_type glad TYPE)
if (library_type STREQUAL "SHARED_LIBRARY")
  target_compile_definitions(glad PRIVATE GLAD_GLAPI_EXPORT)
endif()
