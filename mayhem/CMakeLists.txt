cmake_minimum_required(VERSION 3.16)
project(scpi-parser)

add_executable(fuzzparser fuzz_SCPIParser.c ../examples/common/scpi-def.c)
target_link_libraries(fuzzparser m)
target_link_libraries(fuzzparser ${CMAKE_SOURCE_DIR}/../libscpi/dist/libscpi.a)
target_include_directories(fuzzparser PUBLIC ../libscpi/inc/)
## Uncomment these lines after converting fuzzme.c into a libFuzzer target
#if (NOT CMAKE_CXX_COMPILER_ID STREQUAL "Clang")
#    message(FATAL_ERROR "Clang is required for libFuzzer!")
#endif()
target_compile_options(fuzzparser PUBLIC -fsanitize=fuzzer)
target_link_options(fuzzparser PUBLIC -fsanitize=fuzzer)
