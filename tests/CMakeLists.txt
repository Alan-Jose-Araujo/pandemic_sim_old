include(FetchContent)

# Fetching GoogleTest framework.
FetchContent_Declare(
    googletest
    GIT_REPOSITORY https://github.com/google/googletest.git
    GIT_TAG        v1.15.2
)

# Avoid conflict with the main project flags.
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
set(INSTALL_GTEST OFF CACHE BOOL "" FORCE)

FetchContent_MakeAvailable(googletest)

# Test source files.
add_executable(pandemic_tests
   test_example.cpp
)

target_link_libraries(pandemic_tests
    PRIVATE
        pandemic_core
        GTest::gtest_main
)

include(GoogleTest)
gtest_discover_tests(pandemic_tests)