cmake_minimum_required(VERSION 3.25.0)

project(Gamathon2024)

set(CMAKE_CONFIGURATION_TYPES
    "Debug"
    "RelWithDebInfo"
    "Release"
    CACHE STRING "" FORCE
)

if (NOT DEFINED ARCHITECTURE)
    if (CMAKE_SIZEOF_VOID_P EQUAL 8)
        set(ARCHITECTURE "x86_64")
    elseif(CMAKE_SIZEOF_VOID_P EQUAL 4)
        set(ARCHITECTURE "x86")
    endif()
endif()

if (WIN32)
    set(BUILD_PLATFORM "Windows")
elseif (UNIX)
    set(BUILD_PLATFORM "Linux")
endif()

set_property(GLOBAL PROPERTY USE_FOLDERS ON)

option(ENABLE_SIMD_SSE2 "Enable SSE2 optimizations" OFF)
option(ENABLE_SIMD_SSE3 "Enable SSE3 optimizations" OFF)
option(ENABLE_SIMD_SSSE3 "Enable SSSE3 optimizations" OFF)
option(ENABLE_SIMD_SSE4_1 "Enable SSE 4.1 optimizations" OFF)
option(ENABLE_SIMD_SSE4_2 "Enable SSE 4.2 optimizations" OFF)
option(ENABLE_SIMD_AVX "Enable AVX optimizations" OFF)
option(ENABLE_SIMD_AVX2 "Enable AVX2 optimizations" OFF)

if (ENABLE_SIMD_AVX2)
    set(glaze_ENABLE_AVX2 ON)
endif()

add_subdirectory(Snake3D)
add_subdirectory(thirdparty/raylib)
