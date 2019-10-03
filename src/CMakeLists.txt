# Add all files in src/
file ( GLOB SRC "*.f90" "*.F90" )

## 0. Preprocess ...

# Preprocess every source file
foreach ( "FILE" ${FILES} )
  configure_file ( ${FILE} "${PROJECT_BINARY_DIR}/src/${FILE}" )
  set ( SRC "${PROJECT_BINARY_DIR}/src/${FILE}" ${SRC} )

endforeach ()

## 1. Compile ...

# Include preprocessed source files
include_directories ( "${PROJECT_BINARY_DIR}/src" )

# The main library to build
add_library ( ${CMAKE_PROJECT_NAME} SHARED ${SRC} )

# Where to put files after they are built, and what to name them
set_target_properties ( ${CMAKE_PROJECT_NAME}
  PROPERTIES
  OUTPUT_NAME ${CMAKE_PROJECT_NAME}
  PREFIX lib
  SOVERSION ${VERSION_MAJOR}.${VERSION_MINOR}
  VERSION ${VERSION}
  LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
  Fortran_MODULE_DIRECTORY "${CMAKE_BINARY_DIR}/modules"
)

## 2. Link ...

## 3. Install ...

# Install the compiled library
message ( STATUS "Library install prefix: ${CMAKE_INSTALL_PREFIX}")
install ( TARGETS ${CMAKE_PROJECT_NAME} LIBRARY DESTINATION ${CMAKE_INSTALL_PREFIX}/lib )

# Install FORTRAN module file(s) (in include directory)
install ( DIRECTORY "${CMAKE_BINARY_DIR}/modules/"
	DESTINATION "${CMAKE_INSTALL_PREFIX}/include"
	FILES_MATCHING PATTERN "*.mod"
)
