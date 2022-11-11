cmake_minimum_required(VERSION 3.12)

project(mitsuba)

set(CMAKE_CXX_STANDARD 20)

set(CMAKE_CONFIGURATION_TYPES "Debug;Release;RelWithDebInfo" CACHE STRING "" FORCE)

option(MTS_DEBUG "Enable debug mode" ON)
option(MTS_KD_DEBUG "Enable debug mode for the kd-tree" OFF)
option(MTS_KD_CONSERVE_MEMORY "Use Moeller-Trumbore triangle intersection(48bytes less) instead of Wald intersection" OFF)
option(MTS_SSE "Enable SSE" ON)
option(MTS_HAS_COHERENT_RT "Enable coherent ray tracing" ON)
option(MTS_DEBUG_FP "Enable floating point exceptions" OFF)
option(SPECTRUM_SAMPLES "Number of samples in the spectrum" 3)
option(SINGLE_PRECISION "Use single precision" )
option(DOUBLE_PRECISION "Use double precision" OFF)
option(MTS_GUI_SOFTWARE_FALLBACK "Enable software fallback for GUI" ON)

set(MTS_SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR})
set(MTS_BUILD_DIR ${CMAKE_CURRENT_BINARY_DIR})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/bin)

find_package(Boost 1.74.0 REQUIRED)

if (DOUBLE_PRECISION AND (NOT SINGLE_PRECISION))
    add_compile_definitions(DOUBLE_PRECISION)
    message(STATUS "Using double precision")
elseif (DOUBLE_PRECISION AND SINGLE_PRECISION)
    add_compile_definitions(DOUBLE_PRECISION)
    message(STATUS "Using double precision")
elseif ((NOT DOUBLE_PRECISION) AND SINGLE_PRECISION)
    add_compile_definitions(SINGLE_PRECISION)
    message(STATUS "Using single precision")
else()
    message(FATAL_ERROR "Either SINGLE_PRECISION or DOUBLE_PRECISION must be set")
endif ()

add_subdirectory(src/libcore)
add_subdirectory(src/libhw)
