cmake_minimum_required(VERSION 3.15)
project(Amalgamate)

set(CMAKE_CXX_STANDARD 11)

include_directories(.)

add_executable(Amalgamate
        Amalgamate.cpp
        AppConfig.h
        juce_core_amalgam.cpp
        juce_core_amalgam.h)

target_link_libraries(Amalgamate pthread)

if (MINGW)
    message("now is MINGW")

    if (CMAKE_SIZEOF_VOID_P EQUAL 8)
        message("now is MINGW _WIN64")

        ## ref to juce_core_amalgam.h:812
        target_compile_definitions(Amalgamate PUBLIC JUCE_64BIT)

    endif ()

    ## ref to juce_core_amalgam.cpp:297-305
    target_link_libraries(Amalgamate wsock32 ws2_32)
    target_link_libraries(Amalgamate version)
    target_link_libraries(Amalgamate wininet)
    target_link_libraries(Amalgamate winmm)
    target_link_libraries(Amalgamate shlwapi)
    target_link_libraries(Amalgamate advapi32)


endif ()
