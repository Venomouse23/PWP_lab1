cmake_minimum_required(VERSION 2.6)
project(PierwszyProgram)
add_executable(Laborka main.cpp)
option(USE_TRIGONOMETRY_DEGREE ON)
if (USE_TRIGONOMETRY_DEGREE)
	include_directories("${PROJECT_SOURCE_DIR}/lib")
	add_subdirectory(lib)
	target_link_libraries(Laborka Trygonometria)
endif (USE_TRIGONOMETRY_DEGREE)

configure_file (
"${PROJECT_SOURCE_DIR}/LaborkaConfig.h.in"
"${PROJECT_BINARY_DIR}/LaborkaConfig.h"
)
include_directories("${PROJECT_BINARY_DIR}")

option(BUILD_TESTS "Dodac testy?" ON)
if(BUILD_TESTS)
enable_testing()
add_test(LaborkaPodstawowyTest Laborka)
add_test(LaborkaWynikSin45 Laborka 45)
set_tests_properties(LaborkaWynikSin45 
PROPERTIES PASS_REGULAR_EXPRESSION "0[.,]7071")
add_test(Laborka3sek Laborka)
set_tests_properties(Laborka3sek 
PROPERTIES TIMEOUT 3)
endif(BUILD_TESTS)