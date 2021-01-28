cmake_minimum_required(VERSION 3.10)
project(nanovg)

option(ENABLE_STB "Enable using in-library stb image functions" OFF)

if (NOT ANDROID)
	find_package(PkgConfig REQUIRED)
	pkg_check_modules(GL   REQUIRED IMPORTED_TARGET gl)
	pkg_check_modules(GLU  REQUIRED IMPORTED_TARGET glu)
	pkg_check_modules(GLEW REQUIRED IMPORTED_TARGET glew)

	add_compile_options(
		-D_CRT_SECURE_NO_WARNINGS
		-DNANOVG_GLEW
	)
endif()

if (NOT ENABLE_STB)
	add_compile_options(-DNVG_NO_STB)
endif()

include_directories(${PROJECT_SOURCE_DIR}/src)
add_library(nanovg src/nanovg.c)

if (NOT ANDROID)
	target_link_libraries(nanovg
		PkgConfig::GL
		PkgConfig::GLU
		PkgConfig::GLEW
	)
endif()
