cmake_minimum_required (VERSION 3.28)
project (knet)

set(CMAKE_CXX_STANDARD 17)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)


if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Debug CACHE STRING "Choose the type of build." FORCE)
endif()

include_directories(include)
include_directories(deps/fmt/include)
include_directories(deps/asio)
include_directories(deps/spdlog/include)

if(APPLE)
    set(OPENSSL_ROOT_DIR /usr/local/opt/openssl)
    	FIND_PACKAGE(OpenSSL)
    	if(${OpenSSL_FOUND})
    	  include_directories(${OPENSSL_INCLUDE_DIR})
    	link_directories(${OPENSSL_ROOT_DIR}/lib)
    	endif()
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}  -Wall  -stdlib=libc++  -Wno-unused-function -g  -Wno-deprecated-declarations")
elseif(UNIX)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -pthread   -g -Wno-unused-function -O2  -Wno-unused-variable ")
 
  set(CMAKE_CXX_FLAGS_DEBUG "-g -O0")
  set(CMAKE_CXX_FLAGS_RELEASE "-g -O2")
elseif(WIN32)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}   -D NDEBUG")
endif()
