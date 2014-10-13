project(leptonica)
cmake_minimum_required(VERSION 2.8)

add_subdirectory(src)
add_subdirectory(devtools)
add_subdirectory(prog)

########### install files ###############

configure_file(lept.pc.in lept.pc @ONLY)
install(FILES lept.pc DESTINATION lib/pkgconfig)

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
