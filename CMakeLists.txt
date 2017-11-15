cmake_minimum_required(VERSION 2.8)

project(xrick)

add_subdirectory(zlib)
add_subdirectory(SDL2)
set(SDL_INCLUDE_DIR "${CMAKE_SOURCE_DIR}/SDL2/include")

set(ZLIB_INCLUDE_DIR "${CMAKE_SOURCE_DIR}/zlib" "${CMAKE_BINARY_DIR}/zlib")

include_directories(include)
include_directories(${SDL_INCLUDE_DIR})
include_directories(${ZLIB_INCLUDE_DIR})

file(GLOB_RECURSE sourceFiles src/*.c src/*.e src/*.h include/*.h)

add_executable(xrick ${sourceFiles})

target_link_libraries(xrick ${SDL_LIBRARY})
target_link_libraries(xrick ${ZLIB_LIBRARY})
