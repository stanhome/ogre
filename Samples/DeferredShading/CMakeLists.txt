#-------------------------------------------------------------------
# This file is part of the CMake build system for OGRE
#     (Object-oriented Graphics Rendering Engine)
# For the latest info, see http://www.ogre3d.org/
#
# The contents of this file are placed in the public domain. Feel
# free to make use of it in any way you like.
#-------------------------------------------------------------------

# Configure DeferredShading demo build

set(HEADER_FILES 
  include/AmbientLight.h
  include/DeferredLightCP.h
  include/DeferredShading.h
  include/DeferredShadingDemo.h
  include/DLight.h
  include/GBufferMaterialGenerator.h
  include/GBufferSchemeHandler.h
  include/GeomUtils.h
  include/LightMaterialGenerator.h
  include/ListenerFactoryLogic.h
  include/MaterialGenerator.h
  include/NullSchemeHandler.h
  include/SharedData.h
  include/SSAOLogic.h
)

set(SOURCE_FILES 
  src/AmbientLight.cpp
  src/DeferredLightCP.cpp
  src/DeferredShading.cpp
  src/DeferredShadingDemo.cpp
  src/DLight.cpp
  src/GBufferMaterialGenerator.cpp
  src/GBufferSchemeHandler.cpp
  src/GeomUtils.cpp
  src/LightMaterialGenerator.cpp
  src/MaterialGenerator.cpp
  src/SSAOLogic.cpp
)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
ogre_add_library_to_folder(Samples Sample_DeferredShading ${OGRE_LIB_TYPE} ${SOURCE_FILES} ${HEADER_FILES})

target_link_libraries(Sample_DeferredShading ${OGRE_LIBRARIES} ${SDL2_LIBRARY})
ogre_config_sample_lib(Sample_DeferredShading)

if (APPLE AND NOT APPLE_IOS)
    # Set the INSTALL_PATH so that Samples can be installed in the application package
    set_target_properties(Sample_DeferredShading
       PROPERTIES BUILD_WITH_INSTALL_RPATH 1
       INSTALL_NAME_DIR "@executable_path/../Plugins"
    )
endif()

