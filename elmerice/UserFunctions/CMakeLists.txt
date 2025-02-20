SET(CMAKE_Fortran_MODULE_DIRECTORY
  ${PROJECT_BINARY_DIR}/fmodules CACHE PATH "Directory for Fortran modules")

SET(PROJ "")
SET(ElmerIceUSF_SRC Buoyancy.F90 USF_GetFrictionHeating.F90 USF_Sliding.F90
                    CaffeFlow.F90 USF_LateralFriction.F90 USF_WaterTransfer.F90
                    USF_Contact.F90 USF_ShapeFactor.F90 USF_Zs.F90 USF_Damage.F90
                    USF_Haf.F90 USF_CouplingGlaDS_SSA.F90 USF_CoV.F90 USF_IceProperties.F90
                    USF_GlacierMeshMetric.F90 USF_SourceCalcCalving.F90 ${PROJ})

ADD_LIBRARY(ElmerIceUSF SHARED ${ElmerIceUSF_SRC})
TARGET_LINK_LIBRARIES(ElmerIceUSF Elmer::MPI_Fortran)

IF(HAVE_PROJ)
  SET(PROJ USF_proj.F90)
  INCLUDE_DIRECTORIES(${PROJ_INCLUDE_DIR})
  INCLUDE_DIRECTORIES(${FORTRANGIS_INCLUDE_DIR})
  TARGET_LINK_LIBRARIES(ElmerIceUSF ${PROJ_LIBRARY})
  TARGET_LINK_LIBRARIES(ElmerIceUSF ${FORTRANGIS_LIBRARY})
ENDIF()

# Library object
SET_TARGET_PROPERTIES(ElmerIceUSF PROPERTIES PREFIX "")
IF(NOT(WIN32))
    SET_TARGET_PROPERTIES(ElmerIceUSF PROPERTIES
                          INSTALL_RPATH ${ELMERSOLVER_RPATH_STRING})
ENDIF()
SET_TARGET_PROPERTIES(ElmerIceUSF PROPERTIES
    LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/fem/src/modules
    RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/fem/src/modules)
TARGET_LINK_LIBRARIES(ElmerIceUSF elmersolver ElmerIceUtils)
INSTALL(TARGETS ElmerIceUSF LIBRARY DESTINATION "share/elmersolver/lib"
        RUNTIME DESTINATION "share/elmersolver/lib")
