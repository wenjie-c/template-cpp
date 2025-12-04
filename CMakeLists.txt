CMAKE_MINIMUM_REQUIRED( VERSION 3.16)
project(example VERSION 1.0 DESCRIPTION "Lorem ipsum.")
set(CMAKE_CXX_STANDARD 11)

if(WIN32)
  set(LANGUAGES CXX)
endif()

if(UNIX)
  include(GNUInstallDirs)
endif()

include_directories(include) # Where the libraries headers are
link_directories(lib) # Where the static libraries (xx.a) files are
target_link_libraries(example mylibrary)
set(PROJECT_SOURCE_DIR src)
File(GLOB SRC "${PROJECT_SOURCE_DIR}/*.cpp")
add_executable(example ${SRC})

set_target_properties(example PROPERTIES LINKER_LANGUAGE CXX  VERSION ${PROJECT_VERSION}  OUTPUT_NAME executable)

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Debug)
endif()

set(CMAKE_CXX_FLAGS "-Wall -Wextra")
set(CMAKE_CXX_FLAGS_DEBUG "-g")
set(CMAKE_CXX_FLAGS_RELEASE "-Os") # -DCMAKE_BUILD_TYPE=Release
