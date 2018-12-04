cmake_minimum_required(VERSION 3.8 FATAL_ERROR)

# -----------------------------------------------------------------------------------------------------------------------------
# FILES
# -----------------------------------------------------------------------------------------------------------------------------

# Headers
file(GLOB_RECURSE COMMON_HEADERS ${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/*.h 
                                 ${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/Common/src/*.h 
                                 ${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/Common/include/*.h
                                 ${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/headers/*.h)

# Sources
file(GLOB_RECURSE COMMON_SOURCES ${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/Common/src/*.cpp
                                 ${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src/*.cpp)

if(UNIX OR APPLE OR EMSCRIPTEN)
    list(REMOVE_ITEM COMMON_SOURCES "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/Common/src/windows/CmWindowsDelayLoadHook.cpp")
    list(REMOVE_ITEM COMMON_SOURCES "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/Common/src/windows/CmWindowsModuleUpdateLoader.cpp")
    list(REMOVE_ITEM COMMON_HEADERS "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/Common/include/windows/CmWindowsLoadLibrary.h")
    list(REMOVE_ITEM COMMON_HEADERS "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/Common/include/windows/CmWindowsModuleUpdateLoader.h")
endif()

# if(WIN32 OR APPLE)
#     list(REMOVE_ITEM PHYSX_SOURCES "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysX/src/device/linux/PhysXIndicatorLinux.cpp")
# endif()

# Source groups
source_group("Headers" FILES ${COMMON_HEADERS})
source_group("Sources" FILES ${COMMON_SOURCES})

# -----------------------------------------------------------------------------------------------------------------------------
# TARGETS
# -----------------------------------------------------------------------------------------------------------------------------

add_library(PhysX3Common STATIC ${COMMON_HEADERS} ${COMMON_SOURCES})

if(WIN32)
    target_link_libraries(PhysX3Common "${PROJECT_SOURCE_DIR}/src/Externals/nvToolsExt/1/lib/x64/nvToolsExt64_1.lib")
endif()

target_link_libraries(PhysX3Common PxFoundation)
set_target_properties(PhysX3Common PROPERTIES FOLDER "PhysX")

target_include_directories(PhysX3Common PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/Common/include"
                                               "${PROJECT_SOURCE_DIR}/src/PxShared/include"
                                               "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include"
                                               "${PROJECT_SOURCE_DIR}/src/PxShared/src/fastxml/include"
                                               "${PROJECT_SOURCE_DIR}/src/PxShared/src/pvd/include"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/characterkinematic"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/common"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/extensions"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/geometry"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/GeomUtils"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/pvd"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/cooking"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/particles"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/cloth"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/gpu"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/vehicle"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/Common/src"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/headers"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src/contact"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src/common"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src/convex"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src/distance"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src/sweep"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src/gjk"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src/mesh"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src/hf"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src/pcm"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src/ccd"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src/intersection"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevel/API/include"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevel/software/include"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevel/common/include/pipeline"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevel/common/include/utils"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelAABB/include"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelDynamics/include"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/include"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelDynamics/src"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelParticles/include"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysX/src"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysX/src/buffering"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysX/src/particles"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysX/src/cloth"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/SimulationController/include"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/SimulationController/src"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/SimulationController/src/particles"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/SimulationController/src/cloth"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysXCooking/src"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysXCooking/src/mesh"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysXCooking/src/convex"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/SceneQuery/include"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysXGpu/include"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysXMetaData/core/include"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysXVehicle/src"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysXVehicle/src/PhysXMetaData/include"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysXMetaData/extensions/include"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysXExtensions/src/serialization/Xml"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysXExtensions/src/serialization/File"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysXExtensions/src/serialization/Binary"
                                               "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysXExtensions/src")
