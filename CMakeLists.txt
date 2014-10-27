project(leptonica)
cmake_minimum_required(VERSION 2.8)

if (NO_CONSOLE_IO)
    add_definitions(-DNO_CONSOLE_IO)
endif()

set(ADDHEADERS_DIR_PATH "${CMAKE_BINARY_DIR}/leptonica-include")
set(ADDHEADERS_FILE_PATH "${ADDHEADERS_DIR_PATH}/allheaders.h")

if(WIN32)
    set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /MT")
    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} /MTd /Zi")
    set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} /MT")
    set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} /MTd /Zi")

    # Multithreaded building
    if(MSVC_VERSION GREATER 1400)
        set(PROCESSOR_COUNT "$ENV{NUMBER_OF_PROCESSORS}")
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /MP${PROCESSOR_COUNT}")
        set(CMAKE_C_FLAGS "${CMAKE_CXX_FLAGS} /MP${PROCESSOR_COUNT}")
    endif()
endif()

add_subdirectory(src)
add_subdirectory(devtools)
if(NOT WIN32)
    add_subdirectory(prog)
endif()

########### install files ###############

configure_file(lept.pc.in lept.pc @ONLY)
install(FILES "${CMAKE_CURRENT_BINARY_DIR}/lept.pc" DESTINATION lib/pkgconfig)

# -> share/doc/leptonica
install(
    FILES README.html leptonica-license.txt moller52.jpg version-notes.html
    DESTINATION doc)


#original Makefile.am contents follow:

#EXTRA_DIST = config make-for-auto make-for-local autobuild
#
#pkgconfigdir = $(libdir)/pkgconfig
#pkgconfig_DATA = lept.pc
#
#SUBDIRS = src prog
