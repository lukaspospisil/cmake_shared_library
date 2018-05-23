#*******************************************************************************
#
# compile shared library
#
# USI Lugano, 2018
# lukas.pospisil@usi.ch
#
# *******************************************************************************/
#
# cmake -DCMAKE_CXX_COMPILER=/usr/bin/mpicxx ..
#


cmake_minimum_required(VERSION 2.8.11)

# set default build type
if(NOT CMAKE_BUILD_TYPE)
	set(CMAKE_BUILD_TYPE "Debug")
endif()

# print info about settings
message("\n------------------------------------------------------\n")
message("Compiler ")
message(" - C compiler\t\t\t ${CMAKE_C_COMPILER}")
message(" - C flags\t\t\t ${CMAKE_C_FLAGS}")
message(" - C++ compiler\t\t ${CMAKE_CXX_COMPILER}")
message(" - C++ flags\t\t\t ${CMAKE_CXX_FLAGS}")
message(" - linker\t\t\t ${CMAKE_LINKER}")
message(" - linker flags\t\t ${CMAKE_EXE_LINKER_FLAGS}")
message(" - make\t\t\t ${CMAKE_MAKE_PROGRAM}")
message(" - shared linker flags\t\t ${CMAKE_SHARED_LINKER_FLAGS}")

message("Flags ")
message(" - FLAGS_DEF\t\t\t ${FLAGS_DEF}")
message(" - FLAGS_DEF_D\t\t\t ${FLAGS_DEF_D}")
message(" - LIBRARIES_DEF\t\t ${LIBRARIES_DEF}")
message(" - LIBRARY_PATH\t\t $ENV{LIBRARY_PATH}")

message("\n------------------------------------------------------\n")


# compile shared library
message(STATUS "compiling MYlibrary")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fPIC") # we are compiling shared library

# include header files
include_directories("${CMAKE_SOURCE_DIR}/include")

# create list of targets which will be compiled into library
# the first argument is source dir, the second is dir where it will be compiled
# see CMakeLists.txt in folder "${CMAKE_SOURCE_DIR}/src/" to see what is happening
add_subdirectory("${CMAKE_SOURCE_DIR}/src/" ${CMAKE_BINARY_DIR}/mylibrary)

# the mess of the compilation of the library is stored in "${CMAKE_BINARY_DIR}/mylibrary"
# however, the final library will be stored in lib/ directory 
# (to separate the mess from the final product)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib/")
add_library(mysamplelibrary SHARED $<TARGET_OBJECTS:MYLIBRARY_TARGETS>)

#install(TARGETS mylibrary DESTINATION lib)

