cmake_minimum_required(VERSION 3.10)
project(METIS C)

set(SHARED FALSE CACHE BOOL "build a shared library")

if(MSVC)
  set(METIS_INSTALL FALSE)
else()
  set(METIS_INSTALL TRUE)
endif()

# Configure libmetis library.
if(SHARED)
  set(METIS_LIBRARY_TYPE SHARED)
else()
  set(METIS_LIBRARY_TYPE STATIC)
endif(SHARED)

include(./conf/gkbuild.cmake)

# METIS' custom options
#option(IDX64 "enable 64 bit ints" OFF)
#option(REAL64 "enable 64 bit floats (i.e., double)" OFF)
#if(IDX64)
#  set(METIS_COPTIONS "${METIS_COPTIONS} -DIDXTYPEWIDTH=64")
#else()
#  set(METIS_COPTIONS "${METIS_COPTIONS} -DIDXTYPEWIDTH=32")
#endif(IDX64)
#if(REAL64)
#  set(METIS_COPTIONS "${METIS_COPTIONS} -DREALTYPEWIDTH=64")
#else()
#  set(METIS_COPTIONS "${METIS_COPTIONS} -DREALTYPEWIDTH=32")
#endif(REAL64)
#
#set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${METIS_COPTIONS}")

# set project dir
set(METIS_PATH ${CMAKE_BINARY_DIR}/../)

# set output dir
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${METIS_PATH}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${METIS_PATH}/bin)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${METIS_PATH}/bin)

# set include dir
include_directories(${METIS_PATH}/dependencies/gklib)
include_directories(${METIS_PATH}/dependencies/metis/include)
# Add include directories.
# i.e., the -I equivalent

include_directories(${GKLIB_PATH}/include)
include_directories(${CMAKE_INSTALL_PREFIX}/include)

# List of paths that the compiler will search for library files.
# i.e., the -L equivalent
link_directories(${GKLIB_PATH}/lib)
link_directories(${CMAKE_INSTALL_PREFIX}/lib)

# Recursively look for CMakeLists.txt in subdirs.
add_subdirectory("libmetis")
#add_subdirectory("programs")
