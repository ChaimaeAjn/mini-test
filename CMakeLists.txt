# Version minimale de CMake
cmake_minimum_required(VERSION 3.14)

# Nom du projet
project(MiniTest)

# On utilise C++17
set(CMAKE_CXX_STANDARD 17)

# Notre programme principal
add_executable(MiniTest src/main.cpp)


# =========================
# GoogleTest
# =========================

# Permet à CMake de télécharger GoogleTest
include(FetchContent)

FetchContent_Declare(
    googletest
    URL https://github.com/google/googletest/archive/refs/heads/main.zip
    DOWNLOAD_EXTRACT_TIMESTAMP TRUE
)

FetchContent_MakeAvailable(googletest)


# =========================
# Tests
# =========================

# Active CTest
enable_testing()

# Crée le programme de test
add_executable(
    Tests
    tests/test_main.cpp
)

# Lie GoogleTest à notre programme de test
target_link_libraries(
    Tests
    GTest::gtest_main
)

# Permet à CTest de découvrir automatiquement les tests GoogleTest
include(GoogleTest)
gtest_discover_tests(Tests)