IF(WITH_LUA)
  INCLUDE(test_macros)
  INCLUDE_DIRECTORIES(${CMAKE_BINARY_DIR}/fem/src)

  CONFIGURE_FILE(case.sif case.sif COPYONLY)

  file(COPY ELMERSOLVER_STARTINFO square.msh DESTINATION "${CMAKE_CURRENT_BINARY_DIR}/")

  ADD_ELMER_TEST(MeshSplitLevelset2d LABELS quick lua)
ENDIF(WITH_LUA)
