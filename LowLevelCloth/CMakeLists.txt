# -----------------------------------------------------------------------------------------------------------------------------
# FILES
# -----------------------------------------------------------------------------------------------------------------------------

# Headers
file(GLOB_RECURSE LOWLEVEL_CLOTH_HEADERS ${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/*.h 
                                         ${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/include/*.h 
                                         ${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/*.h)

# Sources
file(GLOB_RECURSE LOWLEVEL_CLOTH_SOURCES ${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/*.cpp)

# Remove AVX sources 
# TODO: Check for AVX support
if(NOT WIN32)
    list(REMOVE_ITEM LOWLEVEL_CLOTH_SOURCES "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/avx/SwSolveConstraints.cpp")
endif()
# Remove NEON sources 
# TODO: Check for NEON support
list(REMOVE_ITEM LOWLEVEL_CLOTH_HEADERS "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/neon/SwCollisionHelpers.h")
list(REMOVE_ITEM LOWLEVEL_CLOTH_SOURCES "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/neon/NeonCollision.cpp"
                                        "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/neon/NeonSelfCollision.cpp"
                                        "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/neon/NeonSolverKernel.cpp")
# Remove Scalar sources
list(REMOVE_ITEM LOWLEVEL_CLOTH_HEADERS "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/scalar/SwCollisionHelpers.h")
# Remove SSE2 source
# TODO: Check for SSE2 support
list(REMOVE_ITEM LOWLEVEL_CLOTH_HEADERS "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/sse2/SwCollisionHelpers.h"
                                        "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/sse2/SwSolveConstraints.h")

# Remove windows-specifc headers
list(REMOVE_ITEM LOWLEVEL_CLOTH_HEADERS "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/windows/ClothClone.h"
                                        "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/windows/CuCheckSuccess.h"
                                        "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/windows/CuCloth.h"
                                        "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/windows/CuClothCreate.h"
                                        "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/windows/CuClothData.h"
                                        "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/windows/CuCollision.h"
                                        "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/windows/CuContextLock.h"
                                        "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/windows/CuDeviceVector.h"
                                        "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/windows/CuFabric.h"
                                        "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/windows/CuFactory.h"
                                        "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/windows/CuPhaseConfig.h"
                                        "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/windows/CuPinnedAllocator.h"
                                        "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/windows/CuSelfCollision.h"
                                        "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/windows/CuSolver.h"
                                        "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/windows/CuSolverKernel.h")
# Remove windows-specific sources
list(REMOVE_ITEM LOWLEVEL_CLOTH_SOURCES "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/windows/CuCloth.cpp"
                                        "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/windows/CuClothClone.cpp"
                                        "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/windows/CuClothCreate.cpp"
                                        "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/windows/CuClothData.cpp"
                                        "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/windows/CuContextLock.cpp"
                                        "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/windows/CuFabric.cpp"
                                        "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/windows/CuFactory.cpp"
                                        "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/windows/CuSolver.cpp")

# if(WIN32 OR APPLE)
#     list(REMOVE_ITEM PHYSX_SOURCES "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysX/src/device/linux/PhysXIndicatorLinux.cpp")
# endif()

# Source groups
source_group("Headers" FILES ${LOWLEVEL_CLOTH_HEADERS})
source_group("Sources" FILES ${LOWLEVEL_CLOTH_SOURCES})

# -----------------------------------------------------------------------------------------------------------------------------
# TARGETS
# -----------------------------------------------------------------------------------------------------------------------------

add_library(LowLevelCloth STATIC ${LOWLEVEL_CLOTH_HEADERS} ${LOWLEVEL_CLOTH_SOURCES})

set_target_properties(LowLevelCloth PROPERTIES FOLDER "PhysX")

target_include_directories(LowLevelCloth PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/Common/include"
                                                "${PROJECT_SOURCE_DIR}/src/PxShared/include"
                                                "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include"
                                                "${PROJECT_SOURCE_DIR}/src/PxShared/src/fastxml/include"
                                                "${PROJECT_SOURCE_DIR}/src/PxShared/src/pvd/include"
                                                "${PROJECT_SOURCE_DIR}/src/PxShared/src/NvSimd/include"
                                                "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/characterkinematic"
                                                "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/common"
                                                "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/extensions"
                                                "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/geometry"
                                                "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/GeomUtils"
                                                "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/pvd"
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
                                                "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevel/common/include/collision"
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

if(WIN32)
    target_include_directories(LowLevelCloth PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src/windows"
                                                    "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/src")
endif()
