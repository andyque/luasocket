
project(luasocket C)
cmake_minimum_required(VERSION 2.8)


if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release CACHE STRING
        "Choose the type of build, options are: None Debug Release RelWithDebInfo MinSizeRel."
        FORCE)
endif()

find_package(Lua51 REQUIRED)
include_directories(${LUA_INCLUDE_DIR})

set(GLOB_RECURSE luasocket_sources "${CMAKE_CURRENT_SOURCE_DIR}/src/*.c")
set(GLOB_RECURSE luasocket_headers "${CMAKE_CURRENT_SOURCE_DIR}/src/*.h")

add_library(libluasocket STATIC ${luasocket_sources})
set_target_properties(libluasocket PROPERTIES PREFIX "")
INSTALL(
  TARGETS libluasocket
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  COMPONENT library
)
install(FILES ${luasocket_headers} DESTINATION "include/luasocket")
# vi:ai et sw=4 ts=4:
