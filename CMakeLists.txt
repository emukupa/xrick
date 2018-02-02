cmake_minimum_required(VERSION 2.8)

project(xrick)

set(ZLIB_EXAMPLE OFF)
set(ZLIB_MINIGZIP OFF)
set(ZLIB_SHARED OFF)
set(SKIP_INSTALL_LIBRARIES ON)
set(SKIP_INSTALL_ALL ON)
add_subdirectory(zlib)
set(ZLIB_INCLUDE_DIR "${CMAKE_SOURCE_DIR}/zlib" "${CMAKE_BINARY_DIR}/zlib")

set(ASSEMBLY OFF)
set(DISKAUDIO OFF)
set(RPATH OFF)
set(SDL_DLOPEN OFF)
set(SSE OFF)
set(PTHREADS OFF)
set(SDL_SHARED OFF)
add_subdirectory(SDL)
set(SDL_INCLUDE_DIR "${CMAKE_SOURCE_DIR}/SDL/include" "${CMAKE_BINARY_DIR}/SDL/include")

include_directories(include)
include_directories(${SDL_INCLUDE_DIR})
include_directories(${ZLIB_INCLUDE_DIR})

file(GLOB_RECURSE sourceFiles src/*.c src/*.e src/*.h include/*.h)

if (EMSCRIPTEN)
	set(CMAKE_EXECUTABLE_SUFFIX ".html")
endif()

add_executable(xrick ${sourceFiles})

target_link_libraries(xrick SDL-static SDLmain)
target_link_libraries(xrick zlibstatic)
