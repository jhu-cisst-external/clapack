#######################################################################
#  This makefile creates the test programs for the BLAS 1 routines.
#  The test files are grouped as follows:
#       SBLAT1 -- Single precision real test routines
#       CBLAT1 -- Single precision complex test routines
#       DBLAT1 -- Double precision real test routines
#       ZBLAT1 -- Double precision complex test routines
#
#  Test programs can be generated for all or some of the four different
#  precisions.  To create the test programs, enter make followed by one
#  or more of the precisions desired.  Some examples:
#       make single
#       make single complex
#       make single double complex complex16
#  Alternatively, the command
#       make
#  without any arguments creates all four test programs.
#  The executable files which are created are called
#       ../xblat1s, ../xblat1d, ../xblat1c, and ../xblat1z
#
#  To remove the object files after the executable files have been
#  created, enter
#       make clean
#  To force the source files to be recompiled, enter, for example,
#       make single FRC=FRC
#
#######################################################################

cmake_policy(SET CMP0026 OLD)

macro(add_blas_test name src)
  get_filename_component(baseNAME ${src} NAME_WE)
  set(TEST_INPUT "${CLAPACK_SOURCE_DIR}/BLAS/${baseNAME}.in")
  add_executable(${name} ${src})
  get_target_property(TEST_LOC ${name} LOCATION)
  target_link_libraries(${name} blas)
  if(EXISTS "${TEST_INPUT}")
    add_test(${name} "${CMAKE_COMMAND}"
      -DTEST=${TEST_LOC}
      -DINPUT=${TEST_INPUT}
      -DINTDIR=${CMAKE_CFG_INTDIR}
      -P "${CLAPACK_SOURCE_DIR}/TESTING/runtest.cmake")
    else()
      add_test(${name} "${CMAKE_COMMAND}" 
        -DTEST=${TEST_LOC}
        -DINTDIR=${CMAKE_CFG_INTDIR}
        -P "${CLAPACK_SOURCE_DIR}/TESTING/runtest.cmake")
    endif()
endmacro(add_blas_test)

add_blas_test(xblat1s sblat1.c)
add_blas_test(xblat1c cblat1.c)
add_blas_test(xblat1d dblat1.c)
add_blas_test(xblat1z zblat1.c)

add_blas_test(xblat2s sblat2.c sblat2.in)
add_blas_test(xblat2c cblat2.c )
add_blas_test(xblat2d dblat2.c)
add_blas_test(xblat2z zblat2.c)

add_blas_test(xblat3s sblat3.c)
add_blas_test(xblat3c cblat3.c)
add_blas_test(xblat3d dblat3.c)
add_blas_test(xblat3z zblat3.c)

