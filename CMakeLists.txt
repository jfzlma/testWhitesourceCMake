cmake_minimum_required(VERSION 3.0 FATAL_ERROR)

# project name and enable C++ support
project(hello LANGUAGES CXX)

# require C++11
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
include(FetchContent)

FetchContent_Declare(json
  GIT_REPOSITORY https://github.com/nlohmann/json.git
  GIT_TAG v3.7.3)

FetchContent_GetProperties(json)
if(NOT json_POPULATED)
  FetchContent_Populate(json)
  add_subdirectory(${json_SOURCE_DIR} ${json_BINARY_DIR} EXCLUDE_FROM_ALL)
endif()



# we define the executable
add_executable(hello main.cc)

# and its sources
#target_sources( hello.x PRIVATE main.cc)
target_link_libraries(hello PRIVATE nlohmann_json::nlohmann_json)