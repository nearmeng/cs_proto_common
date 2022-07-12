cmake_minimum_required (VERSION 3.20)

SET(TARGET_NAME "cs_proto_common")

project(${TARGET_NAME})
list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")

include (proto)
include (fetch_content)

SET(FETCHCONTENT_BASE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/fetch")
fetch_content(thirdparty https://github.com/nearmeng/thirdparty.git master)

SET(BASE_DIR ${CMAKE_CURRENT_SOURCE_DIR})
preprocess_proto(proto)

file (GLOB_RECURSE SRC_FILES "proto/*.cc")

add_library(${TARGET_NAME} STATIC ${SRC_FILES})
add_library(mango::${TARGET_NAME} ALIAS ${TARGET_NAME})

target_include_directories(${TARGET_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
target_link_libraries (${TARGET_NAME}
    3rd::protobuf
)