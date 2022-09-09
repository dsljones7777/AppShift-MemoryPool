project(AppShiftMemoryPool)

set(header_files
	"MemoryPool.h")
set(source_files
	"MemoryPool.cpp")
source_group("Header" FILES ${header_files})
source_group("Source" FILES ${source_files})
set(all_files
	${header_files}
	${source_files})

add_library(${PROJECT_NAME} STATIC ${all_files})

target_include_directories(${PROJECT_NAME} PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}")
target_include_directories(${PROJECT_NAME} PRIVATE "${CMAKE_SOURCE_DIR}/std")
target_include_directories(${PROJECT_NAME} PRIVATE "${CMAKE_SOURCE_DIR}")
target_compile_definitions(${PROJECT_NAME} PRIVATE "free=free_block;malloc=alloc_block;")

if(${CONFIG_APP_SHIFT_MEMORY_POOL_BLOCK_SIZE})
	target_compile_definitions(${PROJECT_NAME} PRIVATE "MEMORYPOOL_DEFAULT_BLOCK_SIZE=${CONFIG_APP_SHIFT_MEMORY_POOL_BLOCK_SIZE};")
endif()

if(MSVC)
	target_link_options(${PROJECT_NAME} PUBLIC
			"/NODEFAULTLIB")
endif()

target_link_libraries(${PROJECT_NAME} PRIVATE Config std)
