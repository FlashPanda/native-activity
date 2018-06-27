cmake_minimum_required(VERSION 3.4.1)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++11 -Wall -Werror")

# 添加bx库
set(bx_dir ../../../../../bx)
add_subdirectory(${bx_dir} bx)

# 添加bimg_decode库
set(bimg_dir ../../../../../bimg)
add_subdirectory(${bimg_dir} bimg)

# 添加dear-imgui库
set(dear-imgui_dir ../../../../../bgfx/3rdparty/dear-imgui)
add_subdirectory(${dear-imgui_dir} dear-imgui)

# 添加ib-compress库
set(ib-compress_dir ../../../../../bgfx/3rdparty/ib-compress)
add_subdirectory(${ib-compress_dir} ib-compress)

# 添加bgfx库
set(bgfx_dir ../../../../../bgfx)
add_subdirectory(${bgfx_dir} bgfx)

# 添加examples-common库
set(examples-common_dir ../../../../../bgfx/examples/common)
add_subdirectory(${examples-common_dir} examples-common)

set(CMAKE_SHARED_LINKER_FLAGS
    "${CMAKE_SHARED_LINKER_FLAGS} -u ANativeActivity_onCreate")

add_library(native-activity SHARED main.cpp)

target_include_directories(native-activity PRIVATE
    ${ANDROID_NDK}/sources/android/native_app_glue
    ${bx_dir}/include
    ${bimg_dir}/include
    ${bgfx_dir}/include
    ${bgfx_dir}/3rdparty
    ${examples-common_dir})

target_link_libraries(native-activity
    bgfx
    examples-common)
