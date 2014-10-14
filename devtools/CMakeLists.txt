
include_directories(${CMAKE_SOURCE_DIR}/src)
add_executable(xtractprotos xtractprotos.c)

# target_link_libraries($(INSTALL_PROGS))

install(TARGETS xtractprotos DESTINATION bin)
target_link_libraries(xtractprotos lept)
