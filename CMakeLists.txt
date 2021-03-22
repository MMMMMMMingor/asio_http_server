cmake_minimum_required(VERSION 2.8.4)
set(CMAKE_VERBOSE_MAKEFILE off)
project(asio_http C CXX)

include_directories(SYSTEM
    deps/asio/asio/include
)
include_directories(
    asio_http/include
    deps/json/single_include
)

add_subdirectory(asio_http)

add_executable(server src/main.cpp)
target_link_libraries(server asio_http)
if (CMAKE_COMPILER_IS_GNUCXX)
    set_target_properties(server PROPERTIES COMPILE_FLAGS "--coverage")
    set_target_properties(server PROPERTIES LINK_FLAGS "--coverage")
endif()
set_property(TARGET server PROPERTY CXX_STANDARD 11)
