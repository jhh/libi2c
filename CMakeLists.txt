cmake_minimum_required(VERSION 3.10)

project(i2c VERSION 1.0.0 DESCRIPTION "Linux i2c library")

add_library(i2c
    SHARED
    src/i2c.c
)
add_library(amaork::i2c ALIAS i2c)

set_target_properties(i2c PROPERTIES VERSION ${PROJECT_VERSION})
set_target_properties(i2c PROPERTIES SOVERSION 1)

set_target_properties(i2c PROPERTIES
    PUBLIC_HEADER src/i2c.h
    LIBRARY_OUTPUT_NAME amaork-i2c
)

include(GNUInstallDirs)

install(
    TARGETS i2c
    EXPORT amaork-i2c
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/amaork
)

install(
    EXPORT amaork-i2c
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/amaork-i2c
    NAMESPACE amaork::
    FILE amaork-i2cConfig.cmake
)