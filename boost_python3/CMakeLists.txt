cmake_minimum_required(VERSION 3.6)
project(boost_python3)

include(ExternalProject)
include(ProcessorCount)
ProcessorCount(N)

find_package(PythonInterp REQUIRED)

ExternalProject_Add(boost_python3-1.66.0
    GIT_REPOSITORY "https://github.com/boostorg/boost"
    GIT_TAG "boost-1.66.0"
    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}
    CONFIGURE_COMMAND bootstrap.bat
    BUILD_COMMAND b2 -j${N} install --with-python --prefix=<INSTALL_DIR> --build-type=complete toolset=msvc-14.1 address-model=64
    BUILD_IN_SOURCE 1
    INSTALL_COMMAND ""
    PATCH_COMMAND cd libs/python && git apply ${CMAKE_CURRENT_LIST_DIR}/builtin_converters.cpp.patch
)
