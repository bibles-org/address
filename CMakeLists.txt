cmake_minimum_required(VERSION 3.30)
project(address)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(address STATIC)

target_sources(address PUBLIC FILE_SET CXX_MODULES FILES
    src/address.cppm
)

target_include_directories(address INTERFACE
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>
    $<INSTALL_INTERFACE:include>
)

include(GNUInstallDirs)

install(TARGETS address
    EXPORT address-targets
    FILE_SET CXX_MODULES DESTINATION ${CMAKE_INSTALL_LIBDIR}/modules
)

install(EXPORT address-targets
    FILE address-config.cmake
    NAMESPACE address::
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/address
)

export(EXPORT address-targets
    FILE "${CMAKE_CURRENT_BINARY_DIR}/address-config.cmake"
    NAMESPACE address::
)
