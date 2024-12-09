cmake_minimum_required(VERSION 3.15)

set(PROJECT_NAME open_interpreter)
project(${PROJECT_NAME} C CXX)

set(CMAKE_CXX_STANDARD 20)

add_executable(client src/main.cpp)

find_package(Boost 1.71.0 COMPONENTS system REQUIRED)
target_include_directories(client PRIVATE ${Boost_INCLUDE_DIR})
target_link_libraries(client Boost::system)

set(THREADS_PREFER_PTHREAD_FLAG ON)
find_package(Threads REQUIRED)
target_link_libraries(client Threads::Threads)

# Add readline library
set(CMAKE_VERBOSE_MAKEFILE on)
include_directories(/usr/include/readline)
file(GLOB SOURCES "./*.c")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c99 -Wall")
target_link_libraries(client readline)