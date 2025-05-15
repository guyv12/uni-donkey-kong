cmake_minimum_required(VERSION 3.15)
project(DonkeyKong2)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

# Sources
file(GLOB_RECURSE SOURCES "src/*.cpp")
add_executable(DonkeyKong2 ${SOURCES})

# SDL2 include path and static .a link
include_directories("${CMAKE_SOURCE_DIR}/libs/SDL2/include")
target_link_libraries(DonkeyKong2
    "${CMAKE_SOURCE_DIR}/src/libSDL2.a"
)

# Copy SDL2.dll and assets
add_custom_command(TARGET DonkeyKong2 POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
        "${CMAKE_SOURCE_DIR}/src/SDL2.dll"
        $<TARGET_FILE_DIR:DonkeyKong2>
    COMMAND ${CMAKE_COMMAND} -E copy_directory
        "${CMAKE_SOURCE_DIR}/assets"
        $<TARGET_FILE_DIR:DonkeyKong2>/assets
)
