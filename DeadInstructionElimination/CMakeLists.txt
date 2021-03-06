cmake_minimum_required(VERSION 3.1)

find_package(LLVM CONFIG REQUIRED)
list(APPEND CMAKE_MODULE_PATH "${LLVM_CMAKE_DIR}")
include(LLVMConfig)

message(STATUS "Found LLVM ${LLVM_PACKAGE_VERSION}")
message(STATUS "Using LLVMConfig.cmake in: ${LLVM_ROOT}/lib/cmake/llvm")
message(STATUS "Looking for LLVM cmake modules: ${LLVM_ROOT}/lib/cmake/llvm")

add_library(dead_code_elimination MODULE
            DeadInstructionElimination.cc
)

include_directories(${LLVM_INCLUDE_DIRS})
include_directories(./include)
add_definitions(${LLVM_DEFINITIONS})

target_compile_features(dead_code_elimination PRIVATE cxx_range_for cxx_auto_type)

set_target_properties(dead_code_elimination PROPERTIES
    COMPILE_FLAGS "-fno-rtti -g"
)
