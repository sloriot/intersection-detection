cmake_minimum_required(VERSION 3.1)
project(intersection-detection)

# set default cmake build type to Release (None Debug Release RelWithDebInfo MinSizeRel)
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release")
endif()

if( APPLE )
	set(LIBS ${LIBS} "-L/opt/local/lib")
	include_directories(/opt/local/include)
else()
	#set(LIBS ${LIBS} "-L/usr/local/lib")
endif()

set(LIBS ${LIBS} "-lsqlite3")

find_package(CGAL)
include(${CGAL_USE_FILE})

if (CGAL_FOUND)
  include_directories(${CGAL_INCLUDE_DIRS})

  set(TET_SOURCES
    convexes.cpp
    gjk.cpp
    kmeans.cpp
    tettest.cpp
    vec.cpp
    CGALStuff.cpp
    )

  add_executable(tet ${TET_SOURCES})
  set_property(TARGET tet PROPERTY CXX_STANDARD 11)
  message("${CGAL_LIBRARY}")
  target_link_libraries (tet CGAL::CGAL ${LIBS})


endif (CGAL_FOUND)
