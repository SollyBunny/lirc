cmake_minimum_required(VERSION 3.10)
project(LIRC C)

set(CMAKE_C_STANDARD 99)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Werror -Wunused -Wextra -Wmaybe-uninitialized -Wstrict-prototypes -Wmissing-prototypes -Wdeclaration-after-statement -Wmissing-declarations -Wmissing-format-attribute -Wnull-dereference -Wformat=2 -Wshadow -Wsizeof-pointer-memaccess -pthread -O3 -g -Wstack-protector -fno-omit-frame-pointer -fwrapv -D_FORTIFY_SOURCE=2")

set(SOURCES irc.c)

add_library(irc SHARED ${SOURCES})
target_link_libraries(irc ssl crypto)

install(DIRECTORY . DESTINATION include/lirc FILES_MATCHING PATTERN "*.h")
install(TARGETS irc LIBRARY DESTINATION lib)

add_executable(irc_client client.c)
target_link_libraries(irc_client irc)

install(TARGETS irc_client RUNTIME DESTINATION bin)
