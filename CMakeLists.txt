cmake_minimum_required(VERSION 3.6)

project(wxwidget-template LANGUAGES CXX)

# allow me build with useful warnings
if (DEFINED DEVEL AND NOT DEVEL EQUAL 0)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Werror") 
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall") 
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wextra") 
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Weffc++") 
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pedantic") 
endif()

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

set(wxWidgets_ROOT_DIR "D:/libraries/wxWidgets")
set(wxWidgets_LIB_DIR "D:/libraries/wxWidgets/lib/gcc_x64_lib")
set(wxWidgets_INCLUDE_DIRS "D:/libraries/wxWidgets/include/")

# Añadir directorios de enlace e inclusión
include_directories(${wxWidgets_INCLUDE_DIRS})
link_directories(${wxWidgets_LIB_DIR})

find_package(wxWidgets REQUIRED COMPONENTS core base)
#find_package(wxWidgets REQUIRED)

if (wxWidgets_FOUND)
  message(STATUS "wxWidgets found: ${wxWidgets_VERSION_STRING}")
  message(STATUS "wxWidgets include dirs: ${wxWidgets_INCLUDE_DIRS}")
  message(STATUS "wxWidgets libraries: ${wxWidgets_LIBRARIES}")
  include(${wxWidgets_USE_FILE})
else()
  message(FATAL_ERROR "wxWidgets not found!")
endif()

add_subdirectory("src")
