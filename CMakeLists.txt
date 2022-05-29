cmake_minimum_required(VERSION 3.0.0)

cmake_path(GET CMAKE_CURRENT_SOURCE_DIR FILENAME dirname)

project(${dirname} VERSION 0.1.0)

add_library(${dirname}
    glad.c
)