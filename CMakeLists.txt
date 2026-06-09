cmake_minimum_required(VERSION 3.10)
project(libprint VERSION 0.1.0.0)
set(CMAKE_CXX_STANDARD 17)

# Опции сборки из файла ci.yml
option(BUILD_EXAMPLES "Build examples" OFF)
option(BUILD_TESTS "Build tests" OFF)

# Библиотека
add_library(print sources/print.cpp)
target_include_directories(print PUBLIC include)

# Исполняемый файл check
add_executable(check tools/check.cpp)

# Сборка примеров, если включен флаг
if(BUILD_EXAMPLES)
    add_executable(example1 examples/example1.cpp)
    add_executable(example2 examples/example2.cpp)
endif()

# Сборка и регистрация тестов, если включен флаг
if(BUILD_TESTS)
    enable_testing()
    add_executable(unit_tests tests/test.cpp)
    target_link_libraries(unit_tests gtest)
    add_test(NAME AllTests COMMAND unit_tests)
endif()

# Модуль установки (target install)
install(TARGETS print check DESTINATION bin)

# Настройка CPack архивации
set(CPACK_GENERATOR "TGZ")
set(CPACK_PACKAGE_NAME "print")
set(CPACK_PACKAGE_VERSION "0.1.0.0")
include(CPack)
