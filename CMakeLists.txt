# CMakeLists files in this project can
# refer to the root source directory of the project as ${HELLO_SOURCE_DIR} and
# to the root binary directory of the project as ${HELLO_BINARY_DIR}.
cmake_minimum_required (VERSION 3.1.0)
project (JonkerVolgenantLib DESCRIPTION "Jonker-Volgenant algorithm to solve the assignement problem in a bipartite graph")

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

set(CMAKE_C_FLAGS "-Wall -Wextra")
set(CMAKE_C_FLAGS_DEBUG "-g")
set(CMAKE_C_FLAGS_RELEASE "-O2")

# Create a library called "Hello" which includes the source file "hello.cxx".
# The extension is already found. Any number of sources could be listed here.
add_library (JonkerVolgenantLib SHARED
                src/assign2DCBasic.c
                src/interface.c
            )

target_compile_options(first-JonkerVolgenantLib PRIVATE -O2)
set_target_properties(JonkerVolgenantLib PROPERTIES PUBLIC_HEADER src/assignAlgs2D.h)
set_property(TARGET JonkerVolgenantLib PROPERTY C_STANDARD 99)
set_property(TARGET JonkerVolgenantLib PROPERTY C_STANDARD_REQUIRED TRUE)
target_include_directories(JonkerVolgenantLib PRIVATE .)
include(GNUInstallDirs)
install(TARGETS JonkerVolgenantLib
    LIBRARY DESTINATION ${prefix}
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})
configure_file(JonkerVolgenantLib.pc.in JonkerVolgenantLib.pc @ONLY)
install(FILES ${CMAKE_BINARY_DIR}/JonkerVolgenantLib.pc
    DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/pkgconfig)
