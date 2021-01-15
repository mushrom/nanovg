cmake_minimum_required(VERSION 3.10)
project(nanovg)

option(ENABLE_STB "Enable using in-library stb image functions" OFF)

find_package(PkgConfig REQUIRED)
pkg_check_modules(GL   REQUIRED IMPORTED_TARGET gl)
pkg_check_modules(GLU  REQUIRED IMPORTED_TARGET glu)
pkg_check_modules(GLEW REQUIRED IMPORTED_TARGET glew)

add_compile_definitions(
	_CRT_SECURE_NO_WARNINGS
	NANOVG_GLEW
)

if (NOT ENABLE_STB)
	add_compile_definitions(NVG_NO_STB)
endif()

include_directories(${PROJECT_SOURCE_DIR}/src)
add_library(nanovg src/nanovg.c)
target_link_libraries(nanovg
	PkgConfig::GL
	PkgConfig::GLU
	PkgConfig::GLEW
)
