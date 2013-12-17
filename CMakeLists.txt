cmake_minimum_required(VERSION 2.6.4)

# Environment Setup ------------------------------------------------------------

# Project Configuration
set(PROJECT_NAME Chihua)
project(${PROJECT_NAME} C CXX)

message(STATUS "AroundKnowledge - Chihuahua")

# Find Dependencies
find_package(Boost 1.41.0
	COMPONENTS
		system
		thread
		unit_test_framework
		date_time
		program_options
	REQUIRED)
find_package(OpenSSL REQUIRED)
find_package(ZLIB REQUIRED)
find_package(Threads REQUIRED)


# Libraries
set(LIBS ${LIBS} ${OPENSSL_LIBRARIES})
set(LIBS ${LIBS} ${ZLIB_LIBRARIES})
set(LIBS ${LIBS} ${CMAKE_THREAD_LIBS_INIT})
set(LIBS ${LIBS} ${Boost_LIBRARIES})

# Includes
set(INCLUDES ${INCLUDES} ${OPENSSL_INCLUDE_DIR} )
set(INCLUDES ${INCLUDES} ${ZLIB_INCLUDE_DIR} )
set(INCLUDES ${INCLUDES} ${Boost_INCLUDE_DIRS} )

# Compiler Flags
set(COMPILER_OPTIONS "-Wall -pedantic")
set(PROJECT_COMPILER_FLAGS "${CMAKE_CXX_FLAGS} ${COMPILER_OPTIONS}")


# Project Setup ----------------------------------------------------------------

# Project directories
set(CHIHUA_SOURCE_DIR "src/")
set(CHIHUA_HEADER_DIR "include/")

# Add project includes.
set(INCLUDES ${INCLUDES} ${CHIHUA_HEADER_DIR})

# Source files patterns
set(CHIHUA_SOURCE_PATTERN "*.c" "*.cpp")
set(CHIHUA_HEADER_PATTERN "*.h" "*.hpp")

# Implementation and declaration files
file(GLOB CHIHUA_SOURCE_FILES ${CHIHUA_SOURCE_DIR}/${CHIHUA_SOURCE_PATTERN})
file(GLOB CHIHUA_HEADER_FILES ${CHIHUA_HEADER_DIR}/${CHIHUA_HEADER_PATTERN})

include_directories(${INCLUDES})
add_executable(${PROJECT_NAME} ${CHIHUA_SOURCE_FILES})

target_link_libraries(${PROJECT_NAME} ${LIBS})

set_property(
  TARGET ${PROJECT_NAME}
  APPEND PROPERTY COMPILE_FLAGS ${PROJECT_COMPILER_FLAGS})









