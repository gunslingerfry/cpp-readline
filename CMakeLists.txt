#    CMakeLists.txt for cpp-readline library
#
#    @author zmij
#    @auther gunslingerfry
#    @date 2021

cmake_minimum_required(VERSION 3.10)
cmake_policy(VERSION 3.10)
project(cpp-readline
    VERSION 0.1.0
    LANGUAGES CXX)
include (GNUInstallDirs)

set (CMAKE_POSITION_INDEPENDENT_CODE ON)

set( CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${PROJECT_SOURCE_DIR}/cmake/modules" )
find_package(Readline REQUIRED)

add_library(${PROJECT_NAME} SHARED
    ${CMAKE_CURRENT_SOURCE_DIR}/src/Console.cpp)
add_library(${PROJECT_NAME}::${PROJECT_NAME} ALIAS ${PROJECT_NAME})

#options
option(BUILD_EXAMPLES "Build example application" ON)

target_include_directories(${PROJECT_NAME}
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include/${PROJECT_NAME}>
        $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
)

set_target_properties(${PROJECT_NAME}
    PROPERTIES
        VERSION ${PROJECT_VERSION}
        SOVERSION 1
        CXX_STANDARD 11
        CXX_STANDARD_REQUIRED ON
        CXX_EXTENSIONS OFF
)
target_link_libraries(${PROJECT_NAME}
    PUBLIC
        Readline::Readline
)

install(TARGETS ${PROJECT_NAME}
    EXPORT ${PROJECT_NAME}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
)

install(EXPORT
    ${PROJECT_NAME}
    FILE ${PROJECT_NAME}-targets.cmake
    DESTINATION ${CMAKE_INSTALL_DATADIR}/${PROJECT_NAME}/cmake
    NAMESPACE ${PROJECT_NAME}::
)
configure_file(
    cmake/${PROJECT_NAME}-config.cmake.in
    ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}/cmake
    @ONLY
)
install(FILES
    ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}-config.cmake
    DESTINATION ${CMAKE_INSTALL_DATADIR}/${PROJECT_NAME}/cmake
)
install(DIRECTORY
    include/${PROJECT_NAME}
    DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
)

# Add subdirectories here
if(BUILD_EXAMPLES)
    add_subdirectory(example)
endif()
