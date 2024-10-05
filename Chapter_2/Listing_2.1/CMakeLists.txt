cmake_minimum_required (VERSION 3.0)
project (TimeIt)

enable_testing()

find_package(MPI)

add_executable(TimeIt TimeIt.c)

add_executable(MPITimeIt MPITimeIt.c)
target_include_directories(MPITimeIt PUBLIC. ${MPI_INCLUDE_PATH})

target_link_libraries(MPITimeIt ${MPI_LIBRARIES})

file(GLOB TESTFILES RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "*.ctest")

foreach(TESTFILE ${TESTFILES})
	add_test(NAME ${TESTFILE} WORKING_DIRECTORY
	${CMAKE_BINARY_DIR}
	COMMAND sh
	${CMAKE_CURRENT_SOURCE_DIR}/${TESTFILE})
endforeach()

add_custom_target(distclean
COMMAND rm -rf CMakeCache.txt CMakeFiles 
CTestTestfile.cmake Makefile Testing
cmake_install.cmake)