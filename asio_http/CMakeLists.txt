cmake_minimum_required(VERSION 2.8.4)
set(CMAKE_VERBOSE_MAKEFILE off)

add_definitions(-DASIO_STANDALONE -DRAPIDJSON_HAS_STDSTRING=1)
file(GLOB SOURCE_FILES src/*.cpp)
add_library(asio_http SHARED ${SOURCE_FILES})
find_package(Threads REQUIRED)
target_link_libraries(asio_http Threads::Threads)
if (CMAKE_COMPILER_IS_GNUCXX)
    set_target_properties(asio_http PROPERTIES COMPILE_FLAGS "--coverage")
    set_target_properties(asio_http PROPERTIES LINK_FLAGS "--coverage")
endif()

set_property(TARGET asio_http PROPERTY CXX_STANDARD 11)
set_property(TARGET asio_http PROPERTY CXX_STANDARD_REQUIRED TRUE)

install(TARGETS asio_http
    LIBRARY DESTINATION ${CMAKE_BINARY_DIR}/lib
)
install(DIRECTORY include/http DESTINATION ${CMAKE_BUILD_DIR}/include)
