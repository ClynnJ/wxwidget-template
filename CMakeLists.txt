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

set(wxWidgets_ROOT_DIR "D:/msys64/mingw64")
set(wxWidgets_LIB_DIR "D:/msys64/mingw64/lib")
set(wxWidgets_LIBRARIES "D:/msys64/mingw64/lib/libwx_mswu-3.2.a")
set(wxWidgets_INCLUDE_DIRS "D:/msys64/mingw64/include/wx-3.2;D:/msys64/mingw64/include;D:/msys64/mingw64/lib/wx/include/msw-unicode-static-3.2")
set(wxWidgets_CONFIGURATION "msw-unicode-static-3.2")

# Añadir directorios de enlace e inclusión
include_directories(${wxWidgets_INCLUDE_DIRS})
link_directories(${wxWidgets_LIB_DIR})

find_package(wxWidgets REQUIRED COMPONENTS monolithic)
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
