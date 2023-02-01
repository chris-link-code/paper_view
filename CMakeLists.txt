cmake_minimum_required(VERSION 3.24)
project(paper_view C)

message("")
message(STATUS "cmake_binary_dir: " ${CMAKE_BINARY_DIR})
message(STATUS "cmake_source_dir: " ${CMAKE_SOURCE_DIR})
message(STATUS "cmake_command: " ${CMAKE_COMMAND})
message(STATUS "cmake_version: " ${CMAKE_VERSION})
message(STATUS "cmake_c_compiler: " ${CMAKE_C_COMPILER})
message(STATUS "cmake_project_name: " ${CMAKE_PROJECT_NAME})
#message(STATUS "cmake_find_cmake: " ${CMAKE_SOURCE_DIR}/CMAKE)

message("")
message(STATUS "project_name: " ${PROJECT_NAME})

set(CMAKE_C_STANDARD 17)

# https://blog.csdn.net/GeiGe123/article/details/113677930
# 设置编译模式，debug/release
#set(CMAKE_BUILD_TYPE "Debug")
# debug/release的编译选项
#set(CMAKE_C_FLAGS_DEBUG "$ENV{CFLAGS} -O0 -Wall -g -ggdb")
#set(CMAKE_C_FLAGS_RELEASE "$ENV{CFLAGS} -O3 -Wall -Wextra -Wpedantic")
# 也可以直接设置编译选项
set(CMAKE_C_FLAGS "-lSDL2 -lX11")

# 隐藏控制台
#set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -mwindows")

# OS
message("")
if (WIN32)
    message("OS is Windows")
elseif (APPLE)
    message("Apple")
elseif (Linux)
    message("linux")
else ()
    message("others")
endif ()

# ------- Set Vars ------- #

#set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
#set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/CMAKE")

# 指定启动代码
set(SOURCE_FILE main.c)
#set(SOURCE_FILE src/basic_setup.c)

message("")
message(STATUS "start source file: " ${SOURCE_FILE})

# ------- End Set Vars --- #


# ------- Executable ----- #

add_executable(paper_view ${SOURCE_FILE})
#ADD_EXECUTABLE(SDL2_Basic_Setup ${SOURCE_FILE})

# ------- End Executable - #


# ------- Finds ---------- #
# finding SDL2
find_package(SDL2 REQUIRED)
message("")
message(STATUS "finding SDL2")
IF (${SDL2_FOUND})
    message(STATUS "SDL2_found: " ${SDL2_FOUND})
    message(STATUS "SDL2_dir: " ${SDL2_DIR})
    message(STATUS "SDL2_include_dir: " ${SDL2_INCLUDE_DIR})
    message(STATUS "SDL2_include_dirs: " ${SDL2_INCLUDE_DIRS})
    message(STATUS "SDL2_libraries: " ${SDL2_LIBRARIES})
    message(STATUS "SDL2_version: " ${SDL2_VERSION})
ELSE ()
    message(FATAL_ERROR "SDL2 NOT FOUND")
ENDIF ()

# finding X11
#[[find_package(X11 REQUIRED)
message("")
message(STATUS "finding X11")
IF (${X11_FOUND})
    message(STATUS "X11_found: " ${X11_FOUND})
    message(STATUS "X11_include_dir: " ${X11_INCLUDE_DIR})
    message(STATUS "X11_libraries: " ${X11_LIBRARIES})
ELSE ()
    message(FATAL_ERROR "X11 NOT FOUND")
ENDIF ()]]

# ------- End Finds ------ #

# ------- Inc & Link ---- #

include_directories(${SDL2_INCLUDE_DIR})
target_link_libraries(
        ${PROJECT_NAME}
        SDL2::SDL2
        SDL2::SDL2main
)


message("")
# ------- End ----------- #