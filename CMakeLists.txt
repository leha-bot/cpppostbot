cmake_minimum_required(VERSION 3.2.2)
project(postbot)

find_package(CURL REQUIRED)

# todo: make some Android-specific conditional statements
option(USE_TO_STRING_HACK "Use the std::to_string hackish implementation on Android NDK" OFF)

if(USE_TO_STRING_HACK)
    add_definitions(-DUSE_TO_STRING_HACK)
endif()

if(MSVC)
	# not tested.
      set(CMAKE_CXX_FLAGS "/O2 /EHsc")
else()
      set(CMAKE_CXX_FLAGS "${CMAKE_C_FLAGS} -O2 -g -std=c++1y")
      # -Wall -Wextra -Werror -pedantic -g -std=c++1y")
endif()

add_executable(rcnbot
    main.cpp
    bot_easy_api.cpp
    bot_network.cpp
    writefn_data.c
)
target_include_directories(rcnbot ${CURL_INCLUDE_DIRS})
target_link_libraries(rcnbot ${CURL_LIBRARIES})
