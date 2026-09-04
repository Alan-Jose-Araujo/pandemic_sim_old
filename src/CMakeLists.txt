# Adding sources to core library.
add_library(
    pandemic_core
    RandomWalkModel.cpp
)

# Adding header files.
target_include_directories(
    pandemic_core
    PUBLIC ${CMAKE_SOURCE_DIR}/include
)

# Linking libraries.
target_link_libraries(
    pandemic_core
    PUBLIC Threads::Threads
)

# Setting the main project executable.
add_executable(
    pandemic_sim
    main.cpp
)
target_link_libraries(
    pandemic_sim
    PRIVATE
    pandemic_core
)