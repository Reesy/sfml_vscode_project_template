cmake_minimum_required(VERSION 3.17.3) 

set(EXECUTABLE_NAME simple_example_application)

project(SFML_PROJ LANGUAGES CXX) #set the project name and to use C++

set(CMAKE_BUILD_TYPE Debug)

set(BUILD_SHARED_LIBS OFF)

set(SFML_STATIC_LIBRARIES ON)

set(MY_SOURCES src/main.cpp)

set(MY_RESOURCES resources)

if(WIN32) # This check detects windows even 64 bit, CMAKE just has a confusing name. 
    add_executable(${EXECUTABLE_NAME} WIN32 ${MY_SOURCES})
    file(COPY ${PROJECT_SOURCE_DIR}/external_resources/SFML/extlibs/bin/x86/openal32.dll DESTINATION ${CMAKE_BINARY_DIR})
    file(COPY ${MY_RESOURCES} DESTINATION ${CMAKE_BINARY_DIR})
elseif(APPLE)
    add_executable(${EXECUTABLE_NAME} ${MY_SOURCES})
    file(COPY ${MY_RESOURCES} DESTINATION ${CMAKE_BINARY_DIR})
endif()

add_subdirectory(${PROJECT_SOURCE_DIR}/external_resources/SFML)

include_directories(${PROJECT_SOURCE_DIR}/external_resources/SFML/include)

target_link_libraries(${EXECUTABLE_NAME} PRIVATE sfml-graphics sfml-audio)
