set(LIBLO_DIR "C:/Users/brady/Documents/GitHub/McGill/liblo")
set(LIBLO_INCLUDES "${LIBLO_DIR}/cmake/build;${LIBLO_DIR}")

#include(UseSWIG)
#find_package(SWIG 4.0 COMPONENTS python)

find_package(SWIG REQUIRED)
include(${SWIG_USE_FILE})

set(Python_ADDITIONAL_VERSIONS 3.5)
find_package(PythonLibs 3)
include_directories(${PYTHON_INCLUDE_DIR})
get_filename_component(PYTHON_LIBRARY_DIR "${PYTHON_LIBRARY}" PATH)
link_directories(${PYTHON_LIBRARY_DIR})

file(GLOB PROJECT_SRC
  "${CMAKE_CURRENT_SOURCE_DIR}/../src/*.h"
  "${CMAKE_CURRENT_SOURCE_DIR}/../src/*.c"
  "${CMAKE_CURRENT_SOURCE_DIR}/../src/*.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/../include/*.h"
)

include_directories(
  "${CMAKE_CURRENT_SOURCE_DIR}"
  "${CMAKE_CURRENT_SOURCE_DIR}/../include"
  "${CMAKE_CURRENT_SOURCE_DIR}/../src"
  "${LIBLO_INCLUDES}"
)

SET(CMAKE_SWIG_FLAGS "")
SET_SOURCE_FILES_PROPERTIES(mapper.i PROPERTIES CPLUSPLUS ON)
#SET_SOURCE_FILES_PROPERTIES(mapper.i PROPERTIES SWIG_FLAGS "-includeall")
swig_add_library(mapper TYPE MODULE LANGUAGE python SOURCES mapper.i ${PROJECT_SRC})
