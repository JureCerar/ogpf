cmake_minimum_required ( VERSION 2.8.8 )
project ( ogpf Fortran )

# Add /cmake subdirectory
list ( APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake" )

# Set project Info, make Public, set Version and define Compiler flags
include ( Colors )
include ( SetVersion )
include ( Info )
include ( Public )
include ( SetCompilerFlags )

# Allow custom Gnuplot executable
if ( GNUPLOT )
	add_definitions ( -D_GNUPLOT=\"${GNUPLOT}\" )
	message ( STATUS "${GREEN}Custom Gnuplot executable set: ${GNUPLOT}${NOR}" )
endif ()

# Main build script
add_subdirectory ( src )

# Tests
enable_testing ()
add_subdirectory ( example )
