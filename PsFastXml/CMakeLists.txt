# -----------------------------------------------------------------------------------------------------------------------------
# FILES
# -----------------------------------------------------------------------------------------------------------------------------

# Headers
file(GLOB_RECURSE PSFASTXML_HEADERS ${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/*.h 
                                    ${PROJECT_SOURCE_DIR}/src/PxShared/src/fastxml/include/*.h)

# Sources
file(GLOB_RECURSE PSFASTXML_SOURCES ${PROJECT_SOURCE_DIR}/src/PxShared/src/fastxml/src/*.cpp)

# Source groups
source_group("Headers" FILES ${PSFASTXML_HEADERS})
source_group("Sources" FILES ${PSFASTXML_SOURCES})

# -----------------------------------------------------------------------------------------------------------------------------
# TARGETS
# -----------------------------------------------------------------------------------------------------------------------------

add_library(PsFastXml STATIC ${PSFASTXML_HEADERS} ${PSFASTXML_SOURCES})

set_target_properties(PsFastXml PROPERTIES FOLDER "PhysX")

target_include_directories(PsFastXml PUBLIC
    "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/Common/include"
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
    "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelParticles/src"
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
