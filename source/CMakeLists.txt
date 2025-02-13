################################################################
cmake_minimum_required(VERSION 3.25)
################################################################
set(LIBRARY_NAME "utf8")
set(LIBRARY_DESC "Library with UTF8 encoder/decoder")

project(libict-${LIBRARY_NAME})

set(CMAKE_CXX_STANDARD 17)
find_package(Threads)

include(../libict-dev-tools/libs-include.cmake)
include(../libict-dev-tools/info-include.cmake)
include(../libict-dev-tools/test-include.cmake)
include(../libict-dev-tools/git-include.cmake)

file(GLOB CMAKE_HEADER_LIST . *.hpp)

set(CMAKE_SOURCE_FILES 
  info.cpp
  robot.cpp
  get.cpp
  transfer.cpp
  stream.cpp
)

add_library(ict-static-${LIBRARY_NAME} STATIC ${CMAKE_SOURCE_FILES})
target_link_libraries(ict-static-${LIBRARY_NAME} ${CMAKE_THREAD_LIBS_INIT})
target_link_libraries(ict-static-${LIBRARY_NAME} ${CMAKE_LINK_LIBS})
set_target_properties(ict-static-${LIBRARY_NAME}  PROPERTIES OUTPUT_NAME ict-${LIBRARY_NAME})

add_library(ict-shared-${LIBRARY_NAME} SHARED ${CMAKE_SOURCE_FILES})
target_link_libraries(ict-shared-${LIBRARY_NAME} ${CMAKE_THREAD_LIBS_INIT})
target_link_libraries(ict-shared-${LIBRARY_NAME} ${CMAKE_LINK_LIBS})
set_target_properties(ict-shared-${LIBRARY_NAME}  PROPERTIES OUTPUT_NAME ict-${LIBRARY_NAME})

add_executable(${PROJECT_NAME}-test test.cpp ${CMAKE_SOURCE_FILES})
target_link_libraries(${PROJECT_NAME}-test ${CMAKE_THREAD_LIBS_INIT})
target_link_libraries(${PROJECT_NAME}-test ${CMAKE_LINK_LIBS})
target_compile_definitions(${PROJECT_NAME}-test PUBLIC -DENABLE_TESTING)
################################################################
install(TARGETS ict-static-${LIBRARY_NAME} ict-shared-${LIBRARY_NAME} DESTINATION lib COMPONENT libraries)
install(
  FILES ${HEADER_LIST}
  DESTINATION include/libict/${LIBRARY_NAME} COMPONENT headers
)
################################################################
enable_testing()

add_test(NAME ict-utf8_robot-tc1 COMMAND ${PROJECT_NAME}-test ict utf8_robot tc1)
add_test(NAME ict-utf8_robot-tc2 COMMAND ${PROJECT_NAME}-test ict utf8_robot tc2)
add_test(NAME ict-utf8_robot-tc3 COMMAND ${PROJECT_NAME}-test ict utf8_robot tc3)
add_test(NAME ict-utf8_robot-tc4 COMMAND ${PROJECT_NAME}-test ict utf8_robot tc4)
add_test(NAME ict-utf8_robot-tc5 COMMAND ${PROJECT_NAME}-test ict utf8_robot tc5)
add_test(NAME ict-utf8_get-tc1 COMMAND ${PROJECT_NAME}-test ict utf8_get tc1)
add_test(NAME ict-utf8_get-tc2 COMMAND ${PROJECT_NAME}-test ict utf8_get tc2)
add_test(NAME ict-utf8_transfer-tc1 COMMAND ${PROJECT_NAME}-test ict utf8_transfer tc1)
add_test(NAME ict-utf8_transfer-tc2 COMMAND ${PROJECT_NAME}-test ict utf8_transfer tc2)
add_test(NAME ict-utf8_transfer-tc3 COMMAND ${PROJECT_NAME}-test ict utf8_transfer tc3)
add_test(NAME ict-utf8_transfer-tc4 COMMAND ${PROJECT_NAME}-test ict utf8_transfer tc4)
add_test(NAME ict-utf8_stream-tc1 COMMAND ${PROJECT_NAME}-test ict utf8_stream tc1)
add_test(NAME ict-utf8_stream-tc2 COMMAND ${PROJECT_NAME}-test ict utf8_stream tc2)
add_test(NAME ict-utf8_stream-tc3 COMMAND ${PROJECT_NAME}-test ict utf8_stream tc3)
add_test(NAME ict-utf8_stream-tc4 COMMAND ${PROJECT_NAME}-test ict utf8_stream tc4)

################################################################
include(../libict-dev-tools/cpack-include.cmake)
################################################################