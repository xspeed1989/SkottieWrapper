cmake_minimum_required(VERSION 3.15)
project(SkottieWrapper)

if(CMAKE_SYSTEM_NAME MATCHES "Linux")
    option(SKIA_USE_CLANG "Use clang to build skia" ON)
endif()

set(SKIA_ROOT ${CMAKE_CURRENT_SOURCE_DIR}/third_party/skia)
set(SKIA_LIBPATH ${CMAKE_CURRENT_SOURCE_DIR}/third_party/skia/out/Skottie)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
endif()

if(${CMAKE_BUILD_TYPE} STREQUAL "Debug")
    message(FATAL_ERROR "${CMAKE_BUILD_TYPE} mode is not supported, because skia issue of debug runtime on windows.")
endif()

message(STATUS "Generated with config types: ${CMAKE_CONFIGURATION_TYPES}")

add_subdirectory(src)
add_subdirectory(third_party)

install(TARGETS SkottieWrapper
        LIBRARY DESTINATION ${CMAKE_INSTALL_PREFIX})

install(DIRECTORY include ${CMAKE_CURRENT_SOURCE_DIR}/include DESTINATION ${CMAKE_INSTALL_PREFIX})