# Check CMake version
cmake_minimum_required(VERSION 3.10)

include("${CMAKE_SOURCE_DIR}/cmake/Obs2Ioda_Functions.cmake")
enable_testing()
include(FetchContent)
# Define the project
project(obs2ioda LANGUAGES Fortran CXX)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_BUILD_TYPE Release)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
# Fortran module output directory for build interface
set(OBS2IODA_MODULE_DIR ${PROJECT_NAME}/module/${CMAKE_Fortran_COMPILER_ID}/${CMAKE_Fortran_COMPILER_VERSION})
# Install Fortran module directory
install(DIRECTORY ${CMAKE_BINARY_DIR}/${OBS2IODA_MODULE_DIR}/ DESTINATION ${CMAKE_INSTALL_LIBDIR}/${OBS2IODA_MODULE_DIR}/)


# Set the Fortran compiler and flags
set(NCEP_BUFR_LIB CACHE STRING "" )
set(BUILD_GOES_ABI_CONVERTER OFF CACHE BOOL "Build the GOES ABI converter")

# Find required packages
find_package(NetCDF REQUIRED COMPONENTS Fortran C CXX)

add_subdirectory("${CMAKE_SOURCE_DIR}/config")
add_subdirectory("${CMAKE_SOURCE_DIR}/src")
add_subdirectory("${CMAKE_SOURCE_DIR}/test")
