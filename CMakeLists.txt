cmake_minimum_required(VERSION 3.15)
project(DonkeyKong2)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

file(GLOB_RECURSE SOURCES "${CMAKE_SOURCE_DIR}/src/*.cpp")

add_executable(DonkeyKong2 ${SOURCES})

include_directories("${CMAKE_SOURCE_DIR}/SDL2-2.0.10/include")

target_link_libraries(DonkeyKong2
    "${CMAKE_SOURCE_DIR}/src/libSDL2.a"
)

# Copy resource directories (textures and levels) to the build output
add_custom_command(TARGET DonkeyKong2 POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory
        "${CMAKE_SOURCE_DIR}/src/DonkeyKongTextures2"
        "$<TARGET_FILE_DIR:DonkeyKong2>/DonkeyKongTextures2"
    COMMAND ${CMAKE_COMMAND} -E copy_directory
        "${CMAKE_SOURCE_DIR}/src/levels"
        "$<TARGET_FILE_DIR:DonkeyKong2>/levels"
    COMMAND ${CMAKE_COMMAND} -E copy
        "${CMAKE_SOURCE_DIR}/src/cs8x8.bmp"
        "$<TARGET_FILE_DIR:DonkeyKong2>/cs8x8.bmp"
)