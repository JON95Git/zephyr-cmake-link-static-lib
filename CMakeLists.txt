cmake_minimum_required(VERSION 3.20.0)

find_package(Zephyr)
project(zephyr_cmake_link_static_lib)

## Add static library
add_library(mylib STATIC IMPORTED GLOBAL)
set_target_properties(mylib PROPERTIES IMPORTED_LOCATION  ${CMAKE_CURRENT_SOURCE_DIR}/mylib/libmylib.a)
set_target_properties(mylib PROPERTIES INTERFACE_INCLUDE_DIRECTORIES ${CMAKE_CURRENT_SOURCE_DIR}/mylib)
target_link_libraries(app INTERFACE mylib)

FILE(GLOB app_sources src/*.c)
target_sources(app PRIVATE ${app_sources})
