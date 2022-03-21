cmake_minimum_required(VERSION 3.14)

project(TestPlan LANGUAGES CXX)

set(CMAKE_PREFIX_PATH "C:\\Qt\\6.2.4\\msvc2019_64\\")

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(QT NAMES Qt6 Qt5 COMPONENTS Core REQUIRED)
find_package(Qt${QT_VERSION_MAJOR} COMPONENTS Core REQUIRED)

add_executable(TestPlan
  main.cpp
)
target_link_libraries(TestPlan Qt${QT_VERSION_MAJOR}::Core)

if(WIN32)
  add_custom_command(
	  TARGET TestPlan POST_BUILD
	  COMMAND ${CMAKE_COMMAND} -E copy_if_different
	  $<TARGET_FILE:Qt${QT_VERSION_MAJOR}::Core>
	  $<TARGET_FILE_DIR:TestPlan>
  )
endif(WIN32)