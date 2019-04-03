cmake_minimum_required(VERSION 3.6)
project(sip)

include(ExternalProject)

find_package(PythonInterp REQUIRED)

ExternalProject_Add(sip-4.19.14
    URL https://www.riverbankcomputing.com/static/Downloads/sip/sip-4.19.14.zip
    URL_MD5 9f17f5714f1cfac8f03e109088b7c44a
    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}
    CONFIGURE_COMMAND
        ${PYTHON_EXECUTABLE} configure.py -d <INSTALL_DIR>/lib/site-packages -e <INSTALL_DIR>/include -b <INSTALL_DIR>/bin --no-dist-info DEFINES+=ROS_BUILD_SHARED_LIBS
    BUILD_COMMAND nmake
    BUILD_IN_SOURCE 1
    INSTALL_COMMAND nmake install
)
