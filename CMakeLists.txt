project(sfa)

cmake_minimum_required(VERSION 2.6)

IF("${PREFIX}" STREQUAL "")
set(PREFIX /usr/local)
endif("${PREFIX}" STREQUAL "")
set(bindir ${PREFIX}/bin)
set(libdir ${PREFIX}/lib)
set(incdir ${PREFIX}/include)

set(MAIN_INC_DIR
  ${CMAKE_SOURCE_DIR}/include)
set(INC_DIRS
  ${MAIN_INC_DIR})

include_directories(${INC_DIRS})

function(addexec name srcs libs)
    add_executable(${name} ${srcs})
    #message("LIBS:" ${libs})
    target_link_libraries(${name} ${libs})
    install(TARGETS ${name} DESTINATION ${bindir})
endfunction(addexec)

function(addlib name libtype srcs libs)
    add_library(${name} ${libtype} ${srcs})
    target_link_libraries(${name} ${libs})
    install(TARGETS ${name} 
                    RUNTIME DESTINATION ${libdir}
                    LIBRARY DESTINATION ${libdir}
                    ARCHIVE DESTINATION ${libdir}
    )
endfunction(addlib)

add_subdirectory(lib)
add_subdirectory(client)
add_subdirectory(tests)
