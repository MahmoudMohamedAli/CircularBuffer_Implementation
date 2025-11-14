cmake_minimum_required(VERSION 3.15)

set(CMAKE_CXX_COMPILER g++)
set(CMAKE_C_COMPILER gcc)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_BUILD_TYPE Debug)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -g ")



project(CircularBuffer)

add_executable(CircularBuffer
   CircularBuffer/CircularBuffer.hpp
)


add_library(CircularBuffer STATIC CircularBuffer/CircularBuffer.hpp)
# include_directories(CircularBuffer "./include")

# add_library(custom_lib_string STATIC
#     src/StringCustom.cpp
# )


# 

# target_include_directories(CircularBuffer PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/CircularBuffer)

# enable_testing()

# add_subdirectory(tests)