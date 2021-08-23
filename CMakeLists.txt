# CMakeLists files in this project can
# refer to the root source directory of the project as ${HELLO_SOURCE_DIR} and
# to the root binary directory of the project as ${HELLO_BINARY_DIR}.
cmake_minimum_required (VERSION 3.1.0)
project (JonkerVolgenant DESCRIPTION "Library for the Jonker-Volgenant algorithm to solve the assignement problem in a bipartite graph")

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

set(CMAKE_C_FLAGS "-Wall -Wextra")
set(CMAKE_C_FLAGS_DEBUG "-g")
set(CMAKE_C_FLAGS_RELEASE "-O2")

# Create a library called "Hello" which includes the source file "hello.cxx".
# The extension is already found. Any number of sources could be listed here.
add_library (JonkerVolgenant SHARED
                src/assign2DCBasic.c
                src/interface.c
            )

target_compile_options(JonkerVolgenant PRIVATE -O2)
set_target_properties(JonkerVolgenant PROPERTIES PUBLIC_HEADER src/assignAlgs2D.h)
set_property(TARGET JonkerVolgenant PROPERTY C_STANDARD 99)
set_property(TARGET JonkerVolgenant PROPERTY C_STANDARD_REQUIRED TRUE)
target_include_directories(JonkerVolgenant PRIVATE .)
include(GNUInstallDirs)
install(TARGETS JonkerVolgenant
    LIBRARY DESTINATION ${prefix}
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})
configure_file(JonkerVolgenant.pc.in JonkerVolgenant.pc @ONLY)
# install(FILES ${CMAKE_BINARY_DIR}/JonkerVolgenant.pc
#     DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/pkgconfig)
install(TARGETS JonkerVolgenant
    RUNTIME DESTINATION lib
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib)
