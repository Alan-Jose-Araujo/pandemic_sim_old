cmake_minimum_required(VERSION 3.20)
project(PandemicSim VERSION 0.1.0 LANGUAGES CXX)

# C++17 standard.
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Compilation database for clangd/IDE.
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Warning flags.
if(CMAKE_CXX_COMPILER_ID MATCHES "GNU|Clang")
    add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# Threads support.
find_package(Threads REQUIRED)

# Debug mode sanitizers.
option(ENABLE_SANITIZERS "Compilar com AddressSanitizer/ThreadSanitizer" OFF)
if(ENABLE_SANITIZERS)
    add_compile_options(-fsanitize=thread -g -O1)
    add_link_options(-fsanitize=thread)
endif()

add_subdirectory(src)

# Testes (enabled by default)
option(BUILD_TESTS "Compilar os testes" ON)
if(BUILD_TESTS)
    enable_testing()
    add_subdirectory(tests)
endif()