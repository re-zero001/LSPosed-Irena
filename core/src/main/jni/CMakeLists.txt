cmake_minimum_required(VERSION 3.28)
project(core)

add_subdirectory(${EXTERNAL_ROOT} external)

aux_source_directory(src SRC_LIST)
aux_source_directory(src/jni SRC_LIST)

add_library(${PROJECT_NAME} STATIC ${SRC_LIST})

target_include_directories(${PROJECT_NAME} PUBLIC include)
target_include_directories(${PROJECT_NAME} PRIVATE src)

set(${PROJECT_NAME}_LINK_LIBS lsplant_static log fmt-header-only)

if (ANDROID_ABI STREQUAL "riscv64")
	set(${PROJECT_NAME}_LINK_LIBS ${${PROJECT_NAME}_LINK_LIBS} rv64hook-static)
else ()
	set(${PROJECT_NAME}_LINK_LIBS ${${PROJECT_NAME}_LINK_LIBS} dobby)
endif ()

target_link_libraries(${PROJECT_NAME} PUBLIC ${${PROJECT_NAME}_LINK_LIBS})
target_link_libraries(${PROJECT_NAME} PRIVATE dex_builder_static)
