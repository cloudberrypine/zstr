cmake_minimum_required(VERSION 3.10 FATAL_ERROR)

project(zstr LANGUAGES CXX)

if (${CMAKE_VERSION} VERSION_GREATER_EQUAL 3.12)
  cmake_policy(SET CMP0074 NEW) # find_package uses <PackageName>_ROOT variables
endif()

if(${CMAKE_VERSION} VERSION_LESS 3.13)
  message(WARNING
    "Interface library targets are not well supported before cmake 3.13  .... "
    "You may need to add \${ZSTR_INCLUDE_DIRS} to your include directories\n"
    "target_include_directories(YourTarget PRIVATE \${ZSTR_INCLUDE_DIRS}) "
  )
endif()

# -- add target

add_library(zstr INTERFACE)
add_library(zstr::zstr ALIAS zstr)

# -- set target properties

target_include_directories(zstr INTERFACE "${PROJECT_SOURCE_DIR}/src")
target_link_libraries(zstr INTERFACE zlibstatic)
target_compile_features(zstr INTERFACE cxx_std_11) # require c++11 flag
