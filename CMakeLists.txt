cmake_minimum_required(VERSION 3.2)

set(APP_NAME gl_boilerplate)

set(SOURCES src/main.c)

## Third party libs
# glad 

add_library(glad STATIC
                 thirdparty/glad/src/glad.c
                 thirdparty/glad/include
)
include_directories(thirdparty/glad/include)

# GLFW

# Building only the GLFW lib
set(BUILD_SHARED_LIBS OFF CACHE BOOL "")
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "")
set(GLFW_BUILD_TESTS OFF CACHE BOOL "")
set(GLFW_BUILD_DOCS OFF CACHE BOOL "")
set(GLFW_INSTALL OFF CACHE BOOL "")

add_subdirectory(thirdparty/glfw)

find_package(OpenGL REQUIRED)

# header only stuff
add_library(header_only_impls STATIC 
                              thirdparty/header_only_impls.c)
include_directories(thirdparty)

##

add_library(gl_utils STATIC
                     lib/gl_utils/src/gl_helpers.c
                     lib/gl_utils/include)
include_directories(lib/gl_utils/include)

add_executable(${APP_NAME} ${SOURCES})
target_link_libraries(${APP_NAME} ${OPENGL_LIBRARIES} glfw glad gl_utils header_only_impls)
