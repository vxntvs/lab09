cmake_minimum_required(VERSION 3.10)
project(libprint VERSION 0.1.0.0)
set(CMAKE_CXX_STANDARD 11)

add_library(print sources/print.cpp)
target_include_directories(print PUBLIC include)

# Включаем модуль CPack для генерации цели "package"
set(CPACK_GENERATOR "TGZ")
set(CPACK_PACKAGE_NAME "print")
set(CPACK_PACKAGE_VERSION "0.1.0.0")
include(CPack)
