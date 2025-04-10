cmake_minimum_required(VERSION 3.8)
project(Algorithm-Visualizer)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
option(BUILD_SHARED_LIBS "Build shared libraries" OFF)

include(FetchContent)
FetchContent_Declare(SFML
    GIT_REPOSITORY https://github.com/SFML/SFML.git
    GIT_TAG 2.6.x
    GIT_SHALLOW ON
    EXCLUDE_FROM_ALL
    SYSTEM)
FetchContent_MakeAvailable(SFML)

add_executable (Algorithm-Visualizer "Algorithm-Visualizer/src/main.cpp" 
                "Algorithm-Visualizer/src/timer.cpp" 
                "Algorithm-Visualizer/src/timer.h" 
                "Algorithm-Visualizer/src/DataPoint.cpp" 
                "Algorithm-Visualizer/src/DataPoint.h"
                "Algorithm-Visualizer/src/SortShape.cpp"
                "Algorithm-Visualizer/src/SortShape.h"
                "Algorithm-Visualizer/src/SortVisualizer.cpp"
                "Algorithm-Visualizer/src/SortVisualizer.h"
                "Algorithm-Visualizer/src/MergeVisualizer.h"
                "Algorithm-Visualizer/src/MergeVisualizer.cpp"
                "Algorithm-Visualizer/src/QuickVisualizer.cpp"
                "Algorithm-Visualizer/src/QuickVisualizer.h")


target_link_libraries(Algorithm-Visualizer PRIVATE sfml-graphics)
target_compile_features(Algorithm-Visualizer PRIVATE cxx_std_17)

set_target_properties(Algorithm-Visualizer PROPERTIES
    VS_DEBUGGER_WORKING_DIRECTORY "$<TARGET_FILE_DIR:Algorithm-Visualizer>")

add_custom_command(TARGET Algorithm-Visualizer POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory
    "${CMAKE_SOURCE_DIR}/Algorithm-Visualizer/resources"
    "$<TARGET_FILE_DIR:Algorithm-Visualizer>/resources"
)

if(WIN32)
    add_custom_command(
        TARGET Algorithm-Visualizer
        COMMENT "Copy OpenAL DLL"
        PRE_BUILD COMMAND ${CMAKE_COMMAND} -E copy ${SFML_SOURCE_DIR}/extlibs/bin/$<IF:$<EQUAL:${CMAKE_SIZEOF_VOID_P},8>,x64,x86>/openal32.dll $<TARGET_FILE_DIR:Algorithm-Visualizer>
        VERBATIM)
endif()