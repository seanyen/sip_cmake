cmake_minimum_required(VERSION 3.6)
project(pyqt5)

include(ExternalProject)

find_package(PythonInterp REQUIRED)
find_package(Qt5 COMPONENTS Core REQUIRED)

get_target_property (QT_QMAKE_EXECUTABLE Qt5::qmake IMPORTED_LOCATION)

ExternalProject_Add(pyqt5-5.10.1
    URL https://sourceforge.net/projects/pyqt/files/PyQt5/PyQt-5.10.1/PyQt5_gpl-5.10.1.zip
    URL_MD5 7bd9ae59c2c4d516dc372577ef344af0
    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}
    CONFIGURE_COMMAND
        ${PYTHON_EXECUTABLE} configure.py --destdir <INSTALL_DIR>/lib/site-packages --bindir <INSTALL_DIR>/bin --no-sip-files --no-tools --qmake ${QT_QMAKE_EXECUTABLE} --confirm-license --verbose
        --sip-incdir ${CMAKE_INSTALL_PREFIX}/include
        --disable QtNfc
        --disable QtX11Extras
        --disable QtWebKit
        --disable QtWebKitWidgets
        --disable QtMacExtras
        --disable QtWebEngine
        --disable QtWebEngineCore
        --disable QtWebEngineWidgets
        --disable QtNetworkAuth
        --disable Enginio
    BUILD_COMMAND nmake
    BUILD_IN_SOURCE 1
    INSTALL_COMMAND nmake install
)
