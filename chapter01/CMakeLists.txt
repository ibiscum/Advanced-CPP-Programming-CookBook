#
# Copyright (C) 2019 Rian Quinn <rianquinn@gmail.com>
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.

# ------------------------------------------------------------------------------
# Header
# ------------------------------------------------------------------------------

cmake_minimum_required(VERSION 3.6)
project(Chapter01)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_FLAGS "-Wall -Wcast-align -Wconversion -Wctor-dtor-privacy -Werror -Wextra -Wpedantic -Wshadow -Wsign-conversion")
# set(CMAKE_CXX_CLANG_TIDY clang-tidy)

# ------------------------------------------------------------------------------
# Recipe 01
# ------------------------------------------------------------------------------

add_custom_target(ch01_rcp01_ex)

function(example number)
    add_executable(ch01_rcp01_ex${number} ch01_rcp01.cpp)
    target_compile_definitions(ch01_rcp01_ex${number} PRIVATE EXAMPLE${number})
    add_dependencies(ch01_rcp01_ex ch01_rcp01_ex${number})
endfunction(example)

example(01)
example(02)
example(03)
example(04)
example(05)
example(06)
example(07)
example(08)
example(09)

# ------------------------------------------------------------------------------
# Recipe 02
# ------------------------------------------------------------------------------

add_custom_target(ch01_rcp02_ex)

function(example number)
    add_executable(ch01_rcp02_ex${number} ch01_rcp02.cpp)
    target_compile_definitions(ch01_rcp02_ex${number} PRIVATE EXAMPLE${number})
    add_dependencies(ch01_rcp02_ex ch01_rcp02_ex${number})
endfunction(example)

example(01)
example(02)

# ------------------------------------------------------------------------------
# Recipe 03
# ------------------------------------------------------------------------------

add_custom_target(recipe03_examples)

file(STRINGS "config.h" CONFIG_H)
file(STRINGS "apis.h" APIS_H)

list(APPEND MY_LIBRARY_SINGLE
    "${CONFIG_H}"
    ""
    "${APIS_H}"
)

file(REMOVE "my_library_single.h")
foreach(LINE IN LISTS MY_LIBRARY_SINGLE)
    if(LINE MATCHES "#include \"")
        file(APPEND "my_library_single.h" "// ${LINE}\n")
    else()
        file(APPEND "my_library_single.h" "${LINE}\n")
    endif()
endforeach()

function(example number)
    add_executable(recipe03_example${number} ch01_recipe03.cpp)
    target_compile_definitions(recipe03_example${number} PRIVATE EXAMPLE${number})
    add_dependencies(recipe03_examples recipe03_example${number})
endfunction(example)

example(01)
example(02)
example(03)
example(04)
example(05)
example(06)
example(07)

# ------------------------------------------------------------------------------
# Recipe 04
# ------------------------------------------------------------------------------

add_custom_target(recipe04_examples)

set(CMAKE_CXX_CLANG_TIDY clang-tidy)

function(example number)
    add_executable(recipe04_example${number} ch01_recipe04.cpp)
    target_compile_definitions(recipe04_example${number} PRIVATE EXAMPLE${number})
    add_dependencies(recipe04_examples recipe04_example${number})
endfunction(example)

example(01)

# ------------------------------------------------------------------------------
# Recipe 05
# ------------------------------------------------------------------------------

add_custom_target(recipe05_examples)

function(example number)
    add_executable(recipe05_example${number} ch01_recipe05.cpp)
    target_compile_definitions(recipe05_example${number} PRIVATE EXAMPLE${number} BOOST_LOG_DYN_LINK)
    add_dependencies(recipe05_examples recipe05_example${number})
    target_link_libraries(recipe05_example${number} boost_chrono boost_log boost_system pthread)
endfunction(example)

example(01)
example(02)

# ------------------------------------------------------------------------------
# Recipe 06
# ------------------------------------------------------------------------------
