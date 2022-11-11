file(GLOB mitsuba_core_hdr "${MTS_SOURCE_DIR}/include/mitsuba/core/*.h")
file(GLOB mitsuba_core_src "${MTS_SOURCE_DIR}/src/libcore/*.cpp")

add_library(mitsuba-core SHARED ${mitsuba_core_src} ${mitsuba_core_hdr})
target_include_directories(mitsuba-core PRIVATE "${MTS_SOURCE_DIR}/include")