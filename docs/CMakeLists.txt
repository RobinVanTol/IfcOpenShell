#Look for an executable called sphinx-build
find_program(SPHINX_EXECUTABLE
             NAMES sphinx-build
             DOC "Path to sphinx-build executable")

include(FindPackageHandleStandardArgs)

#Handle standard arguments to find_package like REQUIRED and QUIET
find_package_handle_standard_args(Sphinx
                                  "Failed to find sphinx-build executable"
                                  SPHINX_EXECUTABLE)

find_package(Doxygen REQUIRED)
#find_package(Sphinx REQUIRED)

set(SPHINX_SOURCE ${CMAKE_CURRENT_SOURCE_DIR})
set(SPHINX_BUILD ${CMAKE_CURRENT_BINARY_DIR}/docs/sphinx)

MESSAGE(STATUS "SPHINX BUILD ${CMAKE_CURRENT_BINARY_DIR}")

file(MAKE_DIRECTORY ./output/doxygen)

if (DOXYGEN_FOUND)

add_custom_target(Sphinx ALL
                  COMMAND
                  ${SPHINX_EXECUTABLE} -v -T -b html
				  ${SPHINX_SOURCE} ${CMAKE_CURRENT_SOURCE_DIR}/output
				  WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/output
                  COMMENT "Generating documentation with Sphinx")
					  
# add_custom_target(ifcopenshell_python_docs ALL
                  # COMMAND make html
                  # WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/../src/ifcblenderexport/docs
				  # OUTPUT ${CMAKE_CURRENT_SOURCE_DIR}/../src/ifcblenderexport/docs
                  # COMMENT "Generating documentation with Sphinx")
	
else (DOXYGEN_FOUND)
  message("Doxygen need to be installed to generate the doxygen documentation")
endif (DOXYGEN_FOUND)
