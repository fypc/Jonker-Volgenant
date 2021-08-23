cmake_minimum_required (VERSION 3.1)
project (JonkerVolgenant    VERSION 1.0
                            DESCRIPTION "Library for the Jonker-Volgenant algorithm to solve the assignement problem in a bipartite graph"
                            LANGUAGES C)

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

set(CMAKE_C_FLAGS "-Wall -Wextra")
set(CMAKE_C_FLAGS_DEBUG "-g")
set(CMAKE_C_FLAGS_RELEASE "-O2")

add_library (JonkerVolgenant SHARED
                src/assign2DCBasic.c
                src/interface.c
            )

            # Enable relative RPATH
if (APPLE)
    set_target_properties(JonkerVolgenantFramework PROPERTIES FRAMEWORK TRUE FRAMEWORK_VERSION C)
elseif (UNIX)
endif()

install(TARGETS JonkerVolgenant DESTINATION lib)
install(TARGETS JonkerVolgenantFramework DESTINATION lib)

