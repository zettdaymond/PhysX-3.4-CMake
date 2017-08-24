cmake_minimum_required(VERSION 3.8 FATAL_ERROR)

# -----------------------------------------------------------------------------------------------------------------------------
# FLAGS
# -----------------------------------------------------------------------------------------------------------------------------

if(APPLE)
    set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -DPX_PHYSX_STATIC_LIB -DNDEBUG -DPX_SUPPORT_PVD=0 -pipe -mmacosx-version-min=10.7 -msse2 -ffast-math -fno-exceptions -fno-rtti -fvisibility=hidden -fvisibility-inlines-hidden -Werror -Wall -Wextra -fstrict-aliasing -Wstrict-aliasing=2 -pedantic -Weverything -Wno-documentation-deprecated-sync -Wno-documentation-unknown-command -Wno-float-equal -Wno-padded -Wno-weak-vtables -Wno-cast-align -Wno-conversion -Wno-missing-variable-declarations -Wno-shift-sign-overflow -Wno-exit-time-destructors -Wno-global-constructors -Wno-missing-prototypes -Wno-unreachable-code -Wno-unused-macros -Wno-used-but-marked-unused -Wno-weak-template-vtables -Wno-invalid-offsetof -Wno-c++11-extensions -O3 -fno-strict-aliasing")
    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -DPX_PHYSX_STATIC_LIB -D_DEBUG -DPX_DEBUG=1 -DPX_CHECKED=1 -DPX_SUPPORT_PVD=1 -pipe -mmacosx-version-min=10.7 -msse2 -ffast-math -fno-exceptions -fno-rtti -fvisibility=hidden -fvisibility-inlines-hidden -Werror -Wall -Wextra -fstrict-aliasing -Wstrict-aliasing=2 -pedantic -Weverything -Wno-documentation-deprecated-sync -Wno-documentation-unknown-command -Wno-float-equal -Wno-padded -Wno-weak-vtables -Wno-cast-align -Wno-conversion -Wno-missing-variable-declarations -Wno-shift-sign-overflow -Wno-exit-time-destructors -Wno-global-constructors -Wno-missing-prototypes -Wno-unreachable-code -Wno-unused-macros -Wno-used-but-marked-unused -Wno-weak-template-vtables -Wno-invalid-offsetof -Wno-c++11-extensions -g3 -gdwarf-2 -O0")
elseif(WIN32)

elseif(EMSCRIPTEN)
    set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -DPX_PHYSX_STATIC_LIB -DNDEBUG -DPX_SUPPORT_PVD=0 -pipe -msse2 -ffast-math -fno-exceptions -fno-rtti -fvisibility=hidden -fvisibility-inlines-hidden -Wno-return-type-c-linkage -Wall -Wextra -fstrict-aliasing -Wstrict-aliasing=2 -pedantic -Weverything -Wno-documentation-deprecated-sync -Wno-documentation-unknown-command -Wno-float-equal -Wno-padded -Wno-weak-vtables -Wno-cast-align -Wno-conversion -Wno-missing-variable-declarations -Wno-shift-sign-overflow -Wno-exit-time-destructors -Wno-global-constructors -Wno-missing-prototypes -Wno-unreachable-code -Wno-unused-macros -Wno-used-but-marked-unused -Wno-weak-template-vtables -Wno-invalid-offsetof -Wno-c++11-extensions -O3 -fno-strict-aliasing")
    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -DPX_PHYSX_STATIC_LIB -D_DEBUG -DPX_DEBUG=1 -DPX_CHECKED=1 -DPX_SUPPORT_PVD=1 -pipe -mmacosx-version-min=10.7 -msse2 -ffast-math -fno-exceptions -fno-rtti -fvisibility=hidden -fvisibility-inlines-hidden -Wno-return-type-c-linkage -Wall -Wextra -fstrict-aliasing -Wstrict-aliasing=2 -pedantic -Weverything -Wno-documentation-deprecated-sync -Wno-documentation-unknown-command -Wno-float-equal -Wno-padded -Wno-weak-vtables -Wno-cast-align -Wno-conversion -Wno-missing-variable-declarations -Wno-shift-sign-overflow -Wno-exit-time-destructors -Wno-global-constructors -Wno-missing-prototypes -Wno-unreachable-code -Wno-unused-macros -Wno-used-but-marked-unused -Wno-weak-template-vtables -Wno-invalid-offsetof -Wno-c++11-extensions -g3 -O0")
endif()

# -----------------------------------------------------------------------------------------------------------------------------
# FILES
# -----------------------------------------------------------------------------------------------------------------------------

# Headers
file(GLOB_RECURSE LOWLEVEL_AABB_HEADERS ${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/*.h 
                                        ${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelAABB/include/*.h 
                                        ${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelAABB/src/*.h)

# Sources
file(GLOB_RECURSE LOWLEVEL_AABB_SOURCES ${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelAABB/src/*.cpp)

# if(UNIX OR APPLE)
#     list(REMOVE_ITEM PHYSX_SOURCES "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysX/src/windows/NpWindowsDelayLoadHook.cpp")
#     list(REMOVE_ITEM PHYSX_SOURCES "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysX/src/device/windows/PhysXIndicatorWindows.cpp")
#     list(REMOVE_ITEM PHYSX_SOURCES "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysX/src/device/windows/PhysXIndicatorWindows.cpp")
# endif()

# if(WIN32 OR APPLE)
#     list(REMOVE_ITEM PHYSX_SOURCES "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysX/src/device/linux/PhysXIndicatorLinux.cpp")
# endif()

# Source groups
source_group("Headers" FILES ${LOWLEVEL_AABB_HEADERS})
source_group("Sources" FILES ${LOWLEVEL_AABB_SOURCES})

# -----------------------------------------------------------------------------------------------------------------------------
# TARGETS
# -----------------------------------------------------------------------------------------------------------------------------

add_library(LowLevelAABB ${LOWLEVEL_AABB_HEADERS} ${LOWLEVEL_AABB_SOURCES})

set_target_properties(LowLevelAABB PROPERTIES FOLDER "PhysX")

target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/Common/include")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PxShared/include")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PxShared/src/fastxml/include")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PxShared/src/pvd/include")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/characterkinematic")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/common")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/extensions")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/geometry")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/GeomUtils")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/pvd")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/particles")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/cloth")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/gpu")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/vehicle")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/Common/src")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/headers")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src/contact")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src/common")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src/convex")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src/distance")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src/sweep")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src/gjk")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src/mesh")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src/hf")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src/pcm")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src/ccd")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/GeomUtils/src/intersection")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevel/API/include")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevel/software/include")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevel/common/include/pipeline")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevel/common/include/utils")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevel/common/include/collision")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelAABB/include")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelDynamics/include")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelCloth/include")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelDynamics/src")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/LowLevelParticles/include")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysX/src")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysX/src/buffering")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysX/src/particles")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysX/src/cloth")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/SimulationController/include")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/SimulationController/src")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/SimulationController/src/particles")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/SimulationController/src/cloth")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysXCooking/src")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysXCooking/src/mesh")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysXCooking/src/convex")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/SceneQuery/include")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysXGpu/include")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysXMetaData/core/include")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysXVehicle/src")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysXVehicle/src/PhysXMetaData/include")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysXMetaData/extensions/include")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysXExtensions/src/serialization/Xml")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysXExtensions/src/serialization/File")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysXExtensions/src/serialization/Binary")
target_include_directories(LowLevelAABB PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/PhysXExtensions/src")