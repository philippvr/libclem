set(CLEM_SOURCES "clem/matrix3x3f_buffer.c" "clem/det3x3.c" "clem/fsum.c")

if(CLEM_BUILD_SHARED_LIBRARY)
  add_library(clem-shared SHARED ${CLEM_SOURCES})
  set_target_properties(clem-shared PROPERTIES OUTPUT_NAME "clem")
  set_property(TARGET clem-shared PROPERTY C_STANDARD 11)

  if(CMAKE_C_NEEDS_LIBM)
    target_link_libraries(clem-shared PRIVATE "m")
  endif()
endif()

if(FSUM_BUILD_STATIC_LIBRARY)
  add_library(clem-static STATIC ${CLEM_SOURCES})
  set_target_properties(clem-static PROPERTIES OUTPUT_NAME "clem")
  set_target_properties(clem-static PROPERTIES PREFIX "lib")
  set_property(TARGET clem-static PROPERTY C_STANDARD 11)

  if(CMAKE_C_NEEDS_LIBM)
    target_link_libraries(clem-static PRIVATE "m")
  endif()
endif()

set(CLEM_SOURCES "${CLEM_SOURCES}" PARENT_SCOPE)
