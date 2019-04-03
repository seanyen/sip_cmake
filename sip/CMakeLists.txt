cmake_minimum_required(VERSION 3.6)
project(sip)

include(ExternalProject)

find_package(PythonInterp REQUIRED)

ExternalProject_Add(sip-4.19.14
    URL https://www.riverbankcomputing.com/static/Downloads/sip/4.19.15/sip-4.19.15.zip
    URL_MD5 4a1a4760cfabef15d68f45a6920974c2
    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}
    CONFIGURE_COMMAND
        ${PYTHON_EXECUTABLE} configure.py -d <INSTALL_DIR>/lib/site-packages -e <INSTALL_DIR>/include -b <INSTALL_DIR>/bin --no-dist-info DEFINES+=ROS_BUILD_SHARED_LIBS
    BUILD_COMMAND nmake
    BUILD_IN_SOURCE 1
    INSTALL_COMMAND nmake install
)
