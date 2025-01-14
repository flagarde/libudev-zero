cmake_minimum_required(VERSION 3.15)

project(libudev-zero)

include(GNUInstallDirs)

set(THREADS_PREFER_PTHREAD_FLAG TRUE)
find_package(Threads)

add_library(libudev-zero
            udev_device.c
            udev_enumerate.c
            udev_hwdb.c
            udev_list.c
            udev_monitor.c
            udev.c
            )

target_compile_options(libudev-zero PRIVATE -D_XOPEN_SOURCE=700)
set_target_properties(libudev-zero PROPERTIES PUBLIC_HEADER "${CMAKE_CURRENT_SOURCE_DIR}/libudev.h")
target_include_directories(libudev-zero PUBLIC $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}> PUBLIC $<INSTALL_INTERFACE:${CMAKE_INSTALL_FULL_INCLUDEDIR}>)
target_link_libraries(libudev-zero PRIVATE Threads::Threads)
install(TARGETS libudev-zero)
