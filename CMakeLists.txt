cmake_minimum_required(VERSION 3.16)
project(kangaroo LANGUAGES CUDA CXX C)

set(CMAKE_CUDA_ARCHITECTURES 86 CACHE STRING "CUDA Architectures")

add_library(kg
Backup.cpp
Check.cpp
Constants.h
HashTable.cpp
HashTable.h
Kangaroo.cpp
Kangaroo.h
Merge.cpp
Network.cpp
PartMerge.cpp
Thread.cpp
Timer.cpp
Timer.h
WindowsErrors.h
SECPK1/Int.cpp
SECPK1/Int.h
SECPK1/IntGroup.cpp
SECPK1/IntGroup.h
SECPK1/IntMod.cpp
SECPK1/Point.cpp
SECPK1/Point.h
SECPK1/Random.cpp
SECPK1/Random.h
SECPK1/SECP256K1.cpp
SECPK1/SECP256k1.h
GPU/GPUCompute.h
GPU/GPUEngine.cu
GPU/GPUEngine.h
GPU/GPUGenerate.cpp
GPU/GPUMath.h
)
target_compile_definitions(kg PUBLIC WITHGPU)
set_source_files_properties(GPU/GPUGenerate.cpp PROPERTIES HEADER_FILE_ONLY TRUE)

if (WIN32)
  target_compile_definitions(kg PUBLIC WIN64)
  target_link_libraries(kg PUBLIC ws2_32)
endif()

add_executable(kangaroo main.cpp)
target_link_libraries(kangaroo kg)
