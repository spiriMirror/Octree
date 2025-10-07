cmake_minimum_required(VERSION 3.10)

project(Octree)

add_library(Octree INTERFACE)

target_compile_features(Octree INTERFACE cxx_std_20)

set(PARENT_DIR ${CMAKE_CURRENT_SOURCE_DIR}/..)

target_include_directories(Octree INTERFACE 
    $<BUILD_INTERFACE:${PARENT_DIR}>
    $<INSTALL_INTERFACE:include>)

file(GLOB OCTREE_HEADERS ${CMAKE_CURRENT_SOURCE_DIR}/*.h)

include(GNUInstallDirs)

install(TARGETS Octree EXPORT OctreeTargets
        RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
        ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
        INCLUDES DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

install(EXPORT OctreeTargets
        FILE OctreeTargets.cmake
        NAMESPACE Octree::
        DESTINATION share/Octree)

install(FILES ${OCTREE_HEADERS} DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/Octree)

install(FILES
    "${PROJECT_SOURCE_DIR}/cmake/OctreeConfig.cmake"
    DESTINATION share/Octree
)
