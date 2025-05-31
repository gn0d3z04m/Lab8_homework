set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
include("cmake/HunterGate.cmake")
HunterGate(
    URL "https://github.com/cpp-pm/hunter/archive/v0.23.251.tar.gz"
    SHA1 "5659b15dc0884d4b03dbd95710e6a1fa0fc3258d"
)
cmake_minimum_required(VERSION 3.5)
project(lab6)
include_directories("formatter_lib/" "formatter_ex_lib/" "solver_lib/")
add_subdirectory(formatter_ex_lib)
add_subdirectory(formatter_lib)
add_subdirectory(solver_lib)
add_subdirectory(solver_application)
add_subdirectory(hello_world_application)
install(TARGETS solva
    RUNTIME DESTINATION bin
    CONFIGURATIONS Release
    DESTINATION bin
    COMPONENT bin
)
install(DIRECTORY "formatter_lib"
    DESTINATION sources
    COMPONENT sources
)
install(DIRECTORY "formatter_ex_lib"
    DESTINATION sources
    COMPONENT sources
)
install(DIRECTORY "formatter_ex_lib"
    DESTINATION sources
    COMPONENT sources
)
install(DIRECTORY "hello_world_application"
    DESTINATION sources
    COMPONENT sources
)
install(DIRECTORY "formatter_ex_lib"
    DESTINATION sources
    COMPONENT sources
)
install(DIRECTORY "solver_application"
    DESTINATION sources
    COMPONENT sources
)
install(DIRECTORY "solver_lib"
    DESTINATION sources
    COMPONENT sources
)

set(CPACK_RPM_PACKAGE_NAME "print-devel")
set(CPACK_RPM_PACKAGE_LICENSE "MIT")
set(CPACK_RPM_PACKAGE_GROUP "print")
set(CPACK_RPM_CHANGELOG_FILE ${CMAKE_CURRENT_SOURCE_DIR}/ChangeLog.md)
set(CPACK_RPM_PACKAGE_RELEASE 1)

set(CPACK_DMG_VOLUME_NAME "Lab6")
set(CPACK_DMG_FORMAT "UDBZ")
set(CPACK_DMG_BACKGROUND_IMAGE "${CMAKE_SOURCE_DIR}/background.png")

set(CPACK_NSIS_MODIFY_PATH ON)
set(CPACK_NSIS_DISPLAY_NAME "Math Solver")
set(CPACK_NSIS_PACKAGE_NAME "Solver ${PROJECT_VERSION}")
set(CPACK_NSIS_CONTACT "support@example.com")

set(CPACK_PACKAGE_INSTALL_DIRECTORY "Pack")
set(CPACK_WIX_PRODUCT_GUID "2ee2d854-75f0-432a-bfa6-8a1ce8fb1c02")
set(CPACK_WIX_UPGRADE_GUID "a1df024f-5ac8-4459-90d0-f5747165dcbd")
set(CPACK_WIX_CMAKE_PACKAGE_REGISTRY TRUE)
set(CPACK_WIX_ARCHITECTURE "x64")

set(CPACK_PACKAGE_NAME "lab6")
set(CPACK_PACKAGE_VERSION "0.1.1")

set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Your name")
set(CPACK_DEBIAN_PACKAGE_DEPENDS "libc6 (>=2.28), zlib1g")
add_custom_target(packageSources
  COMMAND cpack 
    -D CPACK_GENERATOR="ZIP"
    -D CPACK_COMPONENTS_ALL=sources
  COMMAND cpack
    -D CPACK_GENERATOR="TGZ"
    -D CPACK_COMPONENTS_ALL=sources
  COMMENT "Building archives for Component A (ZIP/TGZ)"
)

add_custom_target(packageBin
  COMMAND cpack 
    -D CPACK_GENERATOR="DEB"
    -D CPACK_COMPONENTS_ALL=bin
  COMMENT "Building packages for Component B (DEB/RPM)"
)

add_custom_target(packageBin_RPM
  COMMAND cpack
    -D CPACK_GENERATOR="RPM"
    -D CPACK_COMPONENTS_ALL=bin
)

add_custom_target(packageBin_DMG
  COMMAND cpack
    -D CPACK_GENERATOR="DragNDrop"
    -D CPACK_COMPONENTS_ALL=bin
)

add_custom_target(packageBin_MSI
  COMMAND cpack
    -D CPACK_GENERATOR="WIX"
    -D CPACK_COMPONENTS_ALL=bin
)

add_custom_target(package_all
  DEPENDS
    packageSources
    packageBin
    packageBin_RPM
  COMMENT "Building all packages"
)

set(CPACK_SOURCE_GENERATOR "ZIP")
set(CPACK_DEB_COMPONENT_INSTALL ON)
set(CPACK_RPM_COMPONENT_INSTALL ON)
set(CPACK_WIX_COMPONENT_INSTALL ON)
set(CPACK_DMG_COMPONENT_INSTALL ON)
set(CPACK_COMPONENTS_ALL bin sources)
set(CPACK_ARCHIVE_COMPONENT_INSTALL ON)
include(CPack)
