cmake_minimum_required(VERSION 2.8)

set(HEADERS
	src/Position.h
	src/Board.h
	src/Bot.h
	src/Parser.h
	src/GameEnums.h
	src/RandomBot.h
	src/SnakeitBot.h
	src/LongestBot.h
	src/Logger.h
	src/Optional.h)

set(SOURCES 
	src/Position.cpp
	src/Board.cpp 
	src/Bot.cpp 
	src/Parser.cpp
	src/RandomBot.cpp
	src/SnakeitBot.cpp 
	src/LongestBot.cpp 
	src/Logger.cpp
	main.cpp)

set(USER_LOGS_ENABLED "FALSE" CACHE BOOL "check if debug output is necessary")


if (${USER_LOGS_ENABLED})
	add_definitions(-DLOGS_ENABLED)
endif ()

if (${CMAKE_CXX_COMPILER_ID} STREQUAL "MSVC")
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /std:c++latest")
	add_definitions(-DOPTIONAL_17)
elseif (${CMAKE_CXX_COMPILER_ID} STREQUAL "GNU")
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++1y -static -Isrc -O2 -lm")
else ()
	message(FATAL_ERROR "${CMAKE_CXX_COMPILER_ID} is not supported")
endif ()

add_executable(SnakeIt ${SOURCES} ${HEADERS})
