cmake_minimum_required(VERSION 3.15)

project(CircularBufferExample LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Optionally add debug flags
add_compile_options(-g)

# Enable CMake test functionality
enable_testing()

# Find GoogleTest
find_package(GTest REQUIRED)

if(NOT GTest_FOUND)
    message(FATAL_ERROR "GTest not found")
endif()

# ------------------------------
# Header-only library
# ------------------------------
add_library(CircularBuffer_Lib INTERFACE)


target_include_directories(CircularBuffer_Lib
    INTERFACE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/CircularBuffer>
        $<INSTALL_INTERFACE:include>
)

# ------------------------------
# Test executable
# ------------------------------
set(SRC_FILES
    gTest/functions_Test.cpp
)

add_executable(CircularBuffer_App ${SRC_FILES})

target_link_libraries(CircularBuffer_App
    PRIVATE
        CircularBuffer_Lib
        GTest::gtest
        GTest::gtest_main
        #GTest::gmock_main   # or GTest::gtest_main
)

# ------------------------------
# Register the tests
# ------------------------------
include(GoogleTest)
gtest_discover_tests(CircularBuffer_App)


############################################################
# Install the header-only library
############################################################

# Install public headers
install(
    DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/CircularBuffer
    DESTINATION include
)
install(
    TARGETS CircularBuffer_Lib
    EXPORT CircularBufferTargets
)

############################################################
# Install the application executable
############################################################
install(
    TARGETS CircularBuffer_App
    RUNTIME DESTINATION bin
)

############################################################
# Export the library for find_package()
############################################################
install(
    EXPORT CircularBufferTargets
    FILE CircularBufferConfig.cmake
    NAMESPACE CircularBuffer::
    DESTINATION lib/cmake/CircularBuffer
)