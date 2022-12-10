# Zephyr Cmake link static library
A simple example of how to link a static library to your Zephyr project

## Dependencies

- Zephyr RTOS v3.1.0

## How to generate static library manualy

Generate object file (`.o`)

```bash
arm-none-eabi-gcc -c -o out.o mylib.c
```
Link and generate static library (`.a`)

```bash
arm-none-eabi-ar -rcs libmylib.a out.o
```

## How to add static library to Cmake build system

```cmake
add_library(mylib STATIC IMPORTED GLOBAL)
set_target_properties(mylib PROPERTIES IMPORTED_LOCATION  ${CMAKE_CURRENT_SOURCE_DIR}/mylib/libmylib.a)
set_target_properties(mylib PROPERTIES INTERFACE_INCLUDE_DIRECTORIES ${CMAKE_CURRENT_SOURCE_DIR}/mylib)
target_link_libraries(app INTERFACE mylib)
```