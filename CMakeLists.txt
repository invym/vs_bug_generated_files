
cmake_minimum_required(VERSION 3.10)

project(custom_command)


add_executable(custom_command test.cpp)

add_custom_command(
	OUTPUT ${CMAKE_BINARY_DIR}/generated_test.cpp ${CMAKE_BINARY_DIR}/generated_test.h
	COMMAND ${CMAKE_COMMAND} -E echo "#pragma once" > generated_test.h
	COMMAND ${CMAKE_COMMAND} -E echo "int test();" >> generated_test.h
	COMMAND ${CMAKE_COMMAND} -E echo "#include <generated_test.h>" > generated_test.cpp
	COMMAND ${CMAKE_COMMAND} -E echo "int test() { return 42; }" >> generated_test.cpp
	VERBATIM
)
target_sources(custom_command PRIVATE 
	${CMAKE_BINARY_DIR}/generated_test.h
	${CMAKE_BINARY_DIR}/generated_test.cpp
)
target_include_directories(custom_command PRIVATE ${CMAKE_BINARY_DIR})

