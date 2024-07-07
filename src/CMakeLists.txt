include_directories(.)
include("${wxWidgets_USE_FILE}")

file(GLOB sources *.cpp)

add_executable(${PROJECT_NAME} WIN32 ${sources}) 

target_include_directories(${PROJECT_NAME} PRIVATE ${wxWidgets_INCLUDE_DIRS})
target_link_libraries(${PROJECT_NAME} ${wxWidgets_LIBRARIES})

install(TARGETS ${PROJECT_NAME} RUNTIME DESTINATION bin)
