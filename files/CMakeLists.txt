file(GLOB SOURCES "*.cpp" "*.c")
file(GLOB EMOJIC_DEPEND "*.emojic")

get_filename_component(MAIN_FILE files.emojic ABSOLUTE)
set(PACKAGE_FILE files.o)

add_library(files STATIC ${SOURCES} ${PACKAGE_FILE})
set_property(TARGET files PROPERTY POSITION_INDEPENDENT_CODE ON)
target_compile_options(files PUBLIC -Wall -Wno-unused-result -Wno-missing-braces -pedantic)
add_custom_command(OUTPUT ${PACKAGE_FILE} COMMAND emojicodec -p files -o ${PACKAGE_FILE} -i interface.emojii --color
        -S ${CMAKE_BINARY_DIR} ${MAIN_FILE} DEPENDS emojicodec s ${EMOJIC_DEPEND})
