#*******************************************************************************
#
# compile example which is using shared library
#
# USI Lugano, 2018
# lukas.pospisil@usi.ch
#
# *******************************************************************************/
#

cmake_minimum_required(VERSION 2.8.11)

# set default build type
if(NOT CMAKE_BUILD_TYPE)
	set(CMAKE_BUILD_TYPE "Debug")
endif()

# where is mylibrary? we can provide it using parameter to cmake -DMYLIBRARY_LIB="mylocation"
# but there is some default configuration (because I know where it should be)
set(MYLIBRARY_LIB "${CMAKE_SOURCE_DIR}/../build/lib/" CACHE STRING "directory where MyLibrary is located")
set(MYLIBRARY_INCLUDE "${CMAKE_SOURCE_DIR}/../include/" CACHE STRING "directory header files of MyLibrary")

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

message("Library ")
message(" - MYLIBRARY_LIB\t\t\t ${MYLIBRARY_LIB}")
message(" - MYLIBRARY_INCLUDE\t\t\t ${MYLIBRARY_INCLUDE}")

message("\n------------------------------------------------------\n")


# compile example which uses mylibrary
message(STATUS "compiling myexample")

# include header files of library
include_directories("${MYLIBRARY_INCLUDE}")

# include path where .so with library is located
link_directories("${MYLIBRARY_LIB}")

# add example file 
add_executable(myexample myexample.cpp)

# link shared library (last parameter is the name in MYLIBRARY_LIB folder)
target_link_libraries(myexample LINK_PUBLIC "mysamplelibrary")

