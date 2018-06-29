project(poly2tri)
cmake_minimum_required(VERSION 3.5)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

file(GLOB COMMON_SOURCES poly2tri/common/*.cc)
file(GLOB SWEEP_SOURCES poly2tri/sweep/*.cc)
file(GLOB_RECURSE SOURCE_HEADERS RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} *.h)

set(SOURCE_CC ${COMMON_SOURCES} ${SWEEP_SOURCES})
# set(SOURCE_HEADERS ${COMMON_HEADERS} ${SWEEP_HEADERS})
message("headers: ${SOURCE_HEADERS}")

set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_CURRENT_BINARY_DIR}/lib")
foreach(item ${SOURCE_HEADERS})
    configure_file(${item} "${CMAKE_CURRENT_BINARY_DIR}/include/${item}" COPYONLY)
endforeach(item ${SOURCE_HEADERS})

add_library(poly2tri SHARED ${SOURCE_CC})

target_link_libraries(poly2tri
    m)

target_include_directories(poly2tri PUBLIC
    ${PROJECT_SOURCE_DIR}/poly2tri/common
    ${PROJECT_SOURCE_DIR}/poly2tri/sweep
)