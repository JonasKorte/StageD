cmake_minimum_required(VERSION 3.16)

project("StageD")

set (SOURCES test.cpp)

add_library(staged-core SHARED ${SOURCES})
add_library(staged-core_s STATIC ${SOURCES})

set_target_properties(staged-core_s PROPERTIES OUTPUT_NAME staged-core)