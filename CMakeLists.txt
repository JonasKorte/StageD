cmake_minimum_required(VERSION 3.16)

project("StageD" VERSION 1.0.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)


set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)

set (PLATFORM "default")

if (WIN32)
    set (PLATFORM "win")
    set(shared_install_dest ${CMAKE_SOURCE_DIR}/release/${PLATFORM})
endif()

if (${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
    set (PLATFORM "osx")
    set(CMAKE_INSTALL_RPATH ${CMAKE_INSTALL_RPATH}:/Users/$ENV{USER}/Qt/6.4.1/macos/lib/:${CMAKE_SOURCE_DIR}/release/osx)
    set(CMAKE_BUILD_RPATH ${CMAKE_BUILD_RPATH}:/Users/$ENV{USER}/Qt/6.4.1/macos/lib/:${CMAKE_SOURCE_DIR}/release/osx)
endif()

if (UNIX AND NOT APPLE)
    set (PLATFORM "linux")
endif()

set (install_dest ${CMAKE_SOURCE_DIR}/release/${PLATFORM})
include_directories(${CMAKE_SOURCE_DIR}/api/)

add_subdirectory("staged-core")
install(TARGETS staged-core DESTINATION ${install_dest})
install(TARGETS staged-core_s DESTINATION ${CMAKE_SOURCE_DIR}/lib)

add_subdirectory("staged")
install(TARGETS staged DESTINATION ${install_dest})