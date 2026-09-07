cmake_minimum_required(VERSION 3.20)

project(CreditRiskScorer VERSION 0.1.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

add_executable(credit_risk_scorer
    src/main.cpp
)

target_include_directories(credit_risk_scorer PRIVATE include)

if (MSVC)
    target_compile_options(credit_risk_scorer PRIVATE /W4 /permissive-)
else()
    target_compile_options(credit_risk_scorer PRIVATE -Wall -Wextra -Wpedantic)
endif()

enable_testing()
