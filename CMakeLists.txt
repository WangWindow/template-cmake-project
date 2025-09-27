cmake_minimum_required(VERSION 4.0)
# set(CMAKE_EXPERIMENTAL_CXX_IMPORT_STD d0edc3af-4c50-42ea-a356-e2862fe7a444)
set(CMAKE_SUPPRESS_DEVELOPER_WARNINGS 1 CACHE BOOL "Suppress developer warnings")
set(PROJECT_NAME run)
set(EXECUTABLE run)
project(${PROJECT_NAME} LANGUAGES CXX)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# 设置 C++ 标准
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
# set(CMAKE_CXX_MODULE_STD ON)

# 先创建可执行目标
add_executable(${EXECUTABLE})

# 自动收集 src 目录下所有源文件（含子目录）
file(GLOB_RECURSE SRC_FILES
     CONFIGURE_DEPENDS
     ${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp)

target_sources(${EXECUTABLE}
    PRIVATE
        ${SRC_FILES}
)

target_include_directories(${EXECUTABLE}
    PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/include
)

if (CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
    # 为了启用 std::println 等需要链接额外的库
    target_link_libraries(${EXECUTABLE} stdc++exp)
endif()
