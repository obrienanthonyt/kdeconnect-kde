project(kdeconnect)

set(KDECONNECT_VERSION_MAJOR 0)
set(KDECONNECT_VERSION_MINOR 8)
set(KDECONNECT_VERSION_PATCH 0)
set(KDECONNECT_VERSION "${KDECONNECT_VERSION_MAJOR}.${KDECONNECT_VERSION_MINOR}.${KDECONNECT_VERSION_PATCH}")

cmake_minimum_required(VERSION 2.8.12)

find_package(ECM 0.0.9 REQUIRED NO_MODULE)
set(CMAKE_MODULE_PATH ${ECM_MODULE_PATH} ${ECM_KDE_MODULE_DIR} ${CMAKE_SOURCE_DIR}/cmake)

find_package(Qt5 5.2 REQUIRED COMPONENTS Quick Test)
find_package(KF5 REQUIRED COMPONENTS I18n ConfigWidgets DBusAddons IconThemes)
find_package(Qca-qt5 2.1.0 REQUIRED)

include_directories(${CMAKE_SOURCE_DIR})

configure_file(kdeconnect-version.h.in ${CMAKE_CURRENT_BINARY_DIR}/kdeconnect-version.h)

include(KDEInstallDirs)
include(KDECompilerSettings)
include(KDECMakeSettings)
include(ECMAddTests)
include(ECMSetupVersion)
include(ECMInstallIcons)
include(FeatureSummary)

include(KDEConnectMacros.cmake)

add_definitions(-DQT_NO_URL_CAST_FROM_STRING)

include(GenerateExportHeader)
include_directories(${CMAKE_CURRENT_BINARY_DIR})

add_subdirectory(core)
add_subdirectory(kcm)
add_subdirectory(kcmplugin)
add_subdirectory(kio)
add_subdirectory(icon)
add_subdirectory(interfaces)

add_subdirectory(daemon)
add_subdirectory(plugins)
add_subdirectory(plasmoid)
add_subdirectory(cli)
add_subdirectory(fileitemactionplugin)

add_subdirectory(tests)

install(PROGRAMS kdeconnect-non-plasma.desktop DESTINATION ${XDG_APPS_INSTALL_DIR})
