#-------------------------------------------------------------------
# This file is part of the CMake build system for OGRE
#     (Object-oriented Graphics Rendering Engine)
# For the latest info, see http://www.ogre3d.org/
#
# The contents of this file are placed in the public domain. Feel
# free to make use of it in any way you like.
#-------------------------------------------------------------------

############################################################
# HLMS optional component
############################################################

PROJECT(OgreHLMS)

if(UNIX)
    # this is abused way to much in OgreMain
    add_definitions(-Wno-overloaded-virtual)
endif()

# define header and source files for the library
file(GLOB HEADER_FILES "${CMAKE_CURRENT_SOURCE_DIR}/include/*.h")
file(GLOB SOURCE_FILES "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp")

# Add needed definitions 
add_definitions(-DOGRE_HLMS_EXPORTS)

# include headers
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
include_directories(${OGRE_SOURCE_DIR}/OgreMain/include)

# setup target
ogre_add_library_to_folder(Components OgreHLMS ${OGRE_COMP_LIB_TYPE} ${HEADER_FILES} ${SOURCE_FILES} ${PLATFORM_HEADER_FILES} ${PLATFORM_SOURCE_FILES})
set_target_properties(OgreHLMS PROPERTIES VERSION ${OGRE_SOVERSION} SOVERSION ${OGRE_SOVERSION})
target_link_libraries(OgreHLMS OgreMain)
if (OGRE_CONFIG_THREADS)
  target_link_libraries(OgreHLMS ${OGRE_THREAD_LIBRARIES})
endif ()

# install 
ogre_config_framework(OgreHLMS)
ogre_config_component(OgreHLMS)

install(FILES ${HEADER_FILES}
  DESTINATION include/OGRE/HLMS
)
