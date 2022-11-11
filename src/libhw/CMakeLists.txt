file(GLOB mitsuba_hw_hdr "${MTS_SOURCE_DIR}/include/mitsuba/hw/*.h")
file(GLOB mitsuba_hw_src "${MTS_SOURCE_DIR}/src/libhw/*.cpp")

add_library(mitsuba-hw SHARED ${mitsuba_hw_src} ${mitsuba_hw_hdr})
target_include_directories(mitsuba-hw PRIVATE ${MTS_SOURCE_DIR}/include)