# Module files from the build
include_directories ( ${CMAKE_BINARY_DIR}/modules )

# Testnames
set ( TESTS "demo" )

# Compile all test
foreach ( TESTNAME demo )
  add_executable ( ${TESTNAME} ${TESTNAME}.f90 )
  target_link_libraries ( ${TESTNAME} ogpf )

  # Run test
  add_test ( NAME ${TESTNAME}
    COMMAND echo 0 | ${TESTNAME}
    WORKING_DIRECTORY "${CMAKE_SOURCE_DIR}/example"
  )

endforeach ( TESTNAME )
