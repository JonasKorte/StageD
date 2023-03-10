cmake_minimum_required(VERSION 3.16)

project("StageD" VERSION 1.0.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)

find_package(Qt6 COMPONENTS Widgets Gui Core Qml Quick REQUIRED)

include_directories(${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_CURRENT_BINARY_DIR})
include_directories(${CMAKE_SOURCE_DIR}/staged-core)

if (${PLATFORM} MATCHES "win")
    link_directories(${CMAKE_SOURCE_DIR}/${PLATFORM})
endif()

if (NOT ${PLATFORM} MATCHES "win")
    link_directories(${CMAKE_SOURCE_DIR}/lib)
endif()

set (SOURCES main.cpp)

add_executable(staged ${SOURCES})

target_link_libraries(staged PRIVATE staged-core)