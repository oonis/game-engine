cmake_minimum_required(VERSION 3.13)
project(game_engine)

# Compilation flags
set(CMAKE_CXX_STANDARD 17)
add_definitions(-Wall)

# Load libraries
# GLFW
set(GLFW_BUILD_EXAMPLES OFF CACHE STRING "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE STRING "" FORCE)
set(GLFW_INSTALL OFF CACHE STRING "" FORCE)
add_subdirectory(lib/glfw)
include_directories(lib/glfw/include)

# GLEW
add_definitions(-DGLEW_STATIC)
option(glew-cmake_BUILD_SHARED "" OFF)
add_subdirectory(lib/glew)
include_directories(lib/glew/include lib/glew/src)

# GLM
include_directories(lib/glm)

# Putting it all together
file(GLOB_RECURSE source_files ${PROJECT_SOURCE_DIR}/src/*)
add_executable(main ${source_files})
target_link_libraries(main glfw ${GLFW_LIBRARIES} libglew_static)