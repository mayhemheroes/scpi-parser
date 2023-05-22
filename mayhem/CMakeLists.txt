cmake_minimum_required(VERSION 3.16)
project(scpi-parser)

add_executable(fuzzscpi-parser fuzz_SCPIParser.c ../examples/common/scpi-def.c)
target_link_libraries(fuzzscpi-parser m)
target_link_libraries(fuzzscpi-parser ${CMAKE_SOURCE_DIR}/../libscpi/dist/libscpi.a)
target_include_directories(fuzzscpi-parser PUBLIC ../libscpi/inc/)
## Uncomment these lines after converting fuzzme.c into a libFuzzer target
if (NOT CMAKE_CXX_COMPILER_ID STREQUAL "Clang")
    message(FATAL_ERROR "Clang is required for libFuzzer!")
endif()
target_compile_options(fuzzscpi-parser PUBLIC -fsanitize=fuzzer,address)
target_link_options(fuzzscpi-parser PUBLIC -fsanitize=fuzzer,address)
