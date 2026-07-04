cmake_minimum_required(VERSION 3.10.2)

project(BetaflightPlugin)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

find_package(gz-sim8 REQUIRED)
find_package(gz-plugin2 REQUIRED COMPONENTS register)
find_package(gz-math7 REQUIRED)

add_library(BetaflightPlugin SHARED src/BetaflightPlugin.cc)

set_property(TARGET BetaflightPlugin PROPERTY CXX_STANDARD 17)

target_include_directories(BetaflightPlugin
  PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/src
    ${CMAKE_CURRENT_SOURCE_DIR}/src/comm
)

target_sources(BetaflightPlugin
  PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/src/BetaflightPlugin.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/src/comm/udpsocket.cc
)

target_link_libraries(BetaflightPlugin
  PRIVATE
    gz-sim8::gz-sim8
    gz-plugin2::gz-plugin2
    gz-math7::gz-math7
)