cmake_minimum_required(VERSION 3.6)
project(pyside2)

include(ExternalProject)

find_package(PythonInterp REQUIRED)
find_package(Qt5 COMPONENTS Core REQUIRED)

get_target_property (QT_QMAKE_EXECUTABLE Qt5::qmake IMPORTED_LOCATION)

ExternalProject_Add(pyside2-5.9
    GIT_REPOSITORY "https://code.qt.io/pyside/pyside-setup.git"
    GIT_TAG "5.9"
    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}
    BUILD_IN_SOURCE 1
    CONFIGURE_COMMAND
        ${PYTHON_EXECUTABLE} setup.py install --qmake=${QT_QMAKE_EXECUTABLE}
    BUILD_COMMAND ""
    INSTALL_COMMAND ""
)
