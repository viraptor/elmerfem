IF(HAVE_UMFPACK OR HAVE_MUMPS)
  INCLUDE(${CMAKE_CURRENT_SOURCE_DIR}/../test_macros.cmake)

  CONFIGURE_FILE(ismip_weertman.sif ismip_weertman.sif COPYONLY)

  FILE(COPY ELMERSOLVER_STARTINFO rectangle.grd DESTINATION "${CMAKE_CURRENT_BINARY_DIR}/")

  ADD_ELMERICE_TEST(Friction_Weertman)
  ADD_ELMERICE_LABEL(Friction_Weertman elmerice-fast)
ENDIF()
