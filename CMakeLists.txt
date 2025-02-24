cmake_minimum_required(VERSION 3.25)
project(MathResearch2)

find_package(Boost REQUIRED)
find_package(Catch2 REQUIRED)

set(CMAKE_CXX_STANDARD 20)

#add_subdirectory(third_party/Catch2)
#set(CMAKE_CXX_COMPILER "/opt/homebrew/opt/llvm/bin/clang++")


#set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fopenmp")

# Runner Main executable
add_executable(MathResearch2 runnner_main.cpp Fraction.hpp BloomFilter.hpp Logger.hpp)
target_link_libraries(MathResearch2 PRIVATE Boost::boost)


# Generator Bloom Filter executable
add_executable(MathResearch2_Generator_bf generator_bf_main.cpp Fraction.hpp BloomFilter.hpp Logger.hpp)
target_link_libraries(MathResearch2_Generator_bf PRIVATE Boost::boost)

# Checker Bloom Filter executable
add_executable(MathResearch2_Checker_bf checker_bf_main.cpp Fraction.hpp BloomFilter.hpp Logger.hpp)
target_link_directories(MathResearch2_Checker_bf PRIVATE Boost::boost)

# Test executable
add_executable(MathResearch2_Tests tests/test1.cpp Fraction.hpp tests/FractionTest.cpp tests/BitsetTest.cpp)
target_link_libraries(MathResearch2_Tests PRIVATE Catch2::Catch2WithMain Boost::boost)

add_executable(sample sample.cpp)

include(Ctest)
enable_testing()
add_test(NAME MathResearch2Test COMMAND MathResearch2_Tests)