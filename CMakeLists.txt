
project(luasocket C)
cmake_minimum_required(VERSION 2.8)


if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release CACHE STRING
        "Choose the type of build, options are: None Debug Release RelWithDebInfo MinSizeRel."
        FORCE)
endif()

# find_package(Lua51 REQUIRED)
include_directories(${LUA_INCLUDE_DIR})

# Add lib sources.
set(lib_src
    "src/luasocket.c"
    "src/timeout.c"
    "src/buffer.c"
    "src/io.c"
    "src/auxiliar.c"
    "src/options.c"
    "src/inet.c"
    "src/except.c"
    "src/select.c"
    "src/tcp.c"
    "src/udp.c"
    "src/mime.c"
    "src/luasocket_scripts.c"
)

if(UNIX) # mac, ios, linux, android
  list(APPEND lib_src
    "src/serial.c"
    "src/unix.c"
    "src/usocket.c"
    )
elseif(WIN32)
  list(APPEND lib_src
    "src/wsocket.c"
    )
else()
  message(FATAL_ERROR
    "${CMAKE_CURRENT_LIST_FILE} build on unsupported system ${CMAKE_SYSTEM_NAME}."
    )
endif()
    
file(GLOB_RECURSE luasocket_headers "${CMAKE_CURRENT_SOURCE_DIR}/src/*.h")


add_library(libluasocket STATIC ${lib_src})
set_target_properties(libluasocket PROPERTIES PREFIX "")
INSTALL(
  TARGETS libluasocket
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  COMPONENT library
)
install(FILES ${luasocket_headers} DESTINATION "include/luasocket")
# vi:ai et sw=4 ts=4:
