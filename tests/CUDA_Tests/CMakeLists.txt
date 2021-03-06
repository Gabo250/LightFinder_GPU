project(CUDATests)

enable_language(CXX)

file(GLOB ${PROJECT_NAME}_sources
	"*.cpp" 
	)
	
add_executable(${PROJECT_NAME}
	${${PROJECT_NAME}_sources}
)

target_link_libraries(${PROJECT_NAME} LightFinder_GPU_DLL)
target_link_libraries(${PROJECT_NAME} gtest gtest_main)
target_link_libraries(${PROJECT_NAME} gmock gmock_main)
target_link_libraries(${PROJECT_NAME} TinyXML2)

include_directories(
	${CMAKE_SOURCE_DIR}/sources/dll/headers
	${CMAKE_BINARY_DIR}/googletest-src/googletest/include
	${CMAKE_BINARY_DIR}/googletest-src/googlemock/include
	${CMAKE_SOURCE_DIR}/dependencies/tinyxml2
	)
	
add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
                   COMMAND ${CMAKE_COMMAND} -E copy
                       ${CMAKE_SOURCE_DIR}/resources/In.xml $<TARGET_FILE_DIR:${PROJECT_NAME}>/In.xml)