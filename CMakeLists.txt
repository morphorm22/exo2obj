cmake_minimum_required(VERSION 3.00)

set_property(GLOBAL PROPERTY TARGET_SUPPORTS_SHARED_LIBS TRUE)

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

find_package(SEACASExodus REQUIRED)

set(CMAKE_CXX_STANDARD 14)

project(TEST LANGUAGES CXX)

add_executable(exo2obj src/exo-to-objs-tets-only.cpp)

target_compile_options(exo2obj PRIVATE "-fno-math-errno")
find_library(EXODUS_LIBRARY exodus)
target_link_libraries(exo2obj ${EXODUS_LIBRARY} ${SEACASExodus_TPL_LIBRARIES})
target_include_directories(exo2obj PRIVATE ${SEACASExodus_CXX_FLAGS})

if( CMAKE_INSTALL_PREFIX )
  install( TARGETS exo2obj DESTINATION ${CMAKE_INSTALL_PREFIX}/bin )
endif()

