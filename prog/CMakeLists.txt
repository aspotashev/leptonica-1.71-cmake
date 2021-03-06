
set(INSTALL_PROGS
    convertfilestopdf convertfilestops convertformat convertsegfilestopdf
    convertsegfilestops converttopdf converttops fileinfo printimage
    printsplitimage printtiff splitimage2pdf
)

set(AUTO_REG_PROGS
    alphaops_reg alphaxform_reg bilateral2_reg binarize_reg blackwhite_reg
    blend3_reg blend4_reg colorcontent_reg coloring_reg colormask_reg
    colorquant_reg colorspace_reg compare_reg convolve_reg dewarp_reg dna_reg
    dwamorph1_reg enhance_reg files_reg findcorners_reg findpattern_reg
    fpix1_reg fpix2_reg graymorph2_reg hardlight_reg insert_reg ioformats_reg
    jpegio_reg kernel_reg label_reg maze_reg multitype_reg nearline_reg
    newspaper_reg overlap_reg paint_reg paintmask_reg pdfseg_reg pixa2_reg
    pixserial_reg pngio_reg projection_reg psio_reg psioseg_reg pta_reg
    rankbin_reg rankhisto_reg rasteropip_reg rotate1_reg rotate2_reg
    rotateorth_reg scale_reg seedspread_reg selio_reg shear1_reg shear2_reg
    skew_reg splitcomp_reg subpixel_reg threshnorm_reg translate_reg
    warper_reg writetext_reg xformbox_reg
)

set(MANUAL_REG_PROGS
    alltests_reg adaptnorm_reg affine_reg bilateral1_reg bilinear_reg
    binmorph1_reg binmorph2_reg binmorph3_reg binmorph4_reg binmorph5_reg
    blend1_reg blend2_reg boxa1_reg ccthin1_reg ccthin2_reg cmapquant_reg
    colorize_reg colorseg_reg compfilter_reg conncomp_reg conversion_reg
    distance_reg dwamorph2_reg equal_reg expand_reg extrema_reg fhmtauto_reg
    flipdetect_reg fmorphauto_reg gifio_reg grayfill_reg graymorph1_reg
    grayquant_reg heap_reg jp2kio_reg locminmax_reg logicops_reg lowaccess_reg
    morphseq_reg numa1_reg numa2_reg pixa1_reg pixadisp_reg pixalloc_reg
    pixcomp_reg pixmem_reg pixtile_reg projective_reg ptra1_reg ptra2_reg
    rank_reg rasterop_reg smallpix_reg smoothedge_reg string_reg webpio_reg
    wordboxes_reg
)

set(OTHER_PROGS
    adaptmaptest adaptmap_dark arabic_lines arithtest barcodetest baselinetest
    binarizefiles binarize_set bincompare blendcmaptest buffertest byteatest
    ccbordtest cctest1 colormorphtest colorsegtest colorspacetest comparepages
    comparetest concatpdf contrasttest converttogray convolvetest cornertest
    croptest croptext dewarprules dewarptest1 dewarptest2 dewarptest3
    dewarptest4 digitprep1 displayboxa displaypix displaypixa dithertest
    dwalineargen edgetest falsecolortest fcombautogen fhmtautogen findpattern1
    findpattern2 findpattern3 flipselgen fmorphautogen fpixcontours gammatest
    genfonts graphicstest graymorphtest histotest iotest italictest
    jbcorrelation jbrankhaus jbwords lineremoval listtest livre_adapt
    livre_hmt livre_makefigs livre_orient livre_pageseg livre_seedgen
    livre_tophat maketile misctest1 modifyhuesat morphtest1 mtifftest
    numaranktest otsutest1 otsutest2 pagesegtest1 pagesegtest2 partitiontest
    pdfiotest pixaatest plottest quadtreetest ranktest recogsort recogtest1
    reducetest removecmap renderfonts rotatefastalt rotateorthtest1
    rotatetest1 runlengthtest scaleandtile scaletest1 scaletest2 seedfilltest
    sharptest sheartest showedges skewtest snapcolortest sorttest sudokutest
    trctest viewertest warpertest watershedtest wordsinorder writemtiff
    yuvtest
)

set(ALL_EXECUTABLES
    ${INSTALL_PROGS} ${AUTO_REG_PROGS} ${MANUAL_REG_PROGS} ${OTHER_PROGS})

include_directories("${ALLHEADERS_DIR_PATH}")
include_directories("${CMAKE_SOURCE_DIR}/src")

foreach (PROG ${ALL_EXECUTABLES})
    if ("${PROG}" STREQUAL "dwamorph1_reg" OR "${PROG}" STREQUAL "dwamorph2_reg")
        add_executable(${PROG} ${PROG}.c dwalinear.3.c dwalinearlow.3.c)
    else()
        add_executable(${PROG} ${PROG}.c)
    endif()

    target_link_libraries(${PROG} lept m)
endforeach()

# target_link_libraries($(INSTALL_PROGS))

foreach (PROG ${INSTALL_PROGS})
    install(TARGETS ${PROG} DESTINATION bin)
endforeach()


##########################


#original Makefile.am contents follow:

#AUTOMAKE_OPTIONS = parallel-tests
#AM_CFLAGS = $(DEBUG_FLAGS)
#AM_CPPFLAGS = -I$(top_srcdir)/src
#LDADD = $(top_builddir)/src/liblept.la $(LIBM)
#
#
#
#
#if ENABLE_PROGRAMS
#bin_PROGRAMS = $(INSTALL_PROGS)
#noinst_PROGRAMS = $(AUTO_REG_PROGS) $(MANUAL_REG_PROGS) $(OTHER_PROGS)
#endif
#
#check_PROGRAMS = $(AUTO_REG_PROGS)
#TESTS = $(AUTO_REG_PROGS)
#TESTS_ENVIRONMENT = $(srcdir)/reg_wrapper.sh
#EXTRA_DIST = reg_wrapper.sh
#
#dwamorph1_reg_SOURCES = dwamorph1_reg.c dwalinear.3.c dwalinearlow.3.c
#dwamorph2_reg_SOURCES = dwamorph2_reg.c dwalinear.3.c dwalinearlow.3.c
