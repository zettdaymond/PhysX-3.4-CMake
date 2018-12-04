cmake_minimum_required(VERSION 3.8 FATAL_ERROR)

# -----------------------------------------------------------------------------------------------------------------------------
# PROJECT
# -----------------------------------------------------------------------------------------------------------------------------

project("PhysX")
set_property(GLOBAL PROPERTY USE_FOLDERS ON)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

set (PHYSX_COMMON_DEFINITIONS -DDISABLE_CUDA_PHYSX=1 -DPX_PHYSX_STATIC_LIB=1 -DPX_FOUNDATION_DLL=0 -DPX_PVDSDK_DLL=0)
add_compile_options(
    ${PHYSX_COMMON_DEFINITIONS}
    $<$<CONFIG:Debug>:-DPX_SUPPORT_PVD=0>
    $<$<CONFIG:Debug>:-D_DEBUG=1>
    $<$<NOT:$<CONFIG:Debug>>:-DPX_SUPPORT_PVD=1>
    $<$<NOT:$<CONFIG:Debug>>:-DPX_DEBUG=1>
    $<$<NOT:$<CONFIG:Debug>>:-DPX_CHECKED=1>
    $<$<NOT:$<CONFIG:Debug>>:-DNDEBUG=1>
)

if(WIN32)
    add_definitions(-D_CRT_SECURE_NO_DEPRECATE -D_CRT_NONSTDC_NO_DEPRECATE -D_WINSOCK_DEPRECATED_NO_WARNINGS)
    add_compile_options(/Zc:wchar_t /GF /GR- /Zc:forScope /Wall /wd4514 /wd4820 /wd4127 /wd4710 /wd4711 /wd4435 /wd4577 /wd4464 /wd5045 /d2Zi+)
else()
    if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
        add_compile_options(-Wno-return-type-c-linkage -Wno-documentation-deprecated-sync
            -Wno-documentation-unknown-command -Wno-weak-vtables -Wno-missing-variable-declarations
            -Wno-shift-sign-overflow -Wno-exit-time-destructors -Wno-global-constructors -Wno-used-but-marked-unused
            -Wno-c++11-extensions
        )
    endif ()
    add_compile_options(-pipe -msse2 -ffast-math -fno-exceptions -fno-rtti -fno-strict-aliasing -Wno-float-equal
        -Wno-padded -Wno-cast-align -Wno-conversion -Wno-unreachable-code -Wno-unused-macros -Wno-invalid-offsetof)
endif()

# -----------------------------------------------------------------------------------------------------------------------------
# SUB-DIRECTORIES
# -----------------------------------------------------------------------------------------------------------------------------                    

# PhysX Library
add_subdirectory("PhysX")
add_subdirectory("PhysXCharacterKinematic")
add_subdirectory("PhysXVehicle")
add_subdirectory("PhysXExtensions")
add_subdirectory("SceneQuery")
add_subdirectory("SimulationController")
add_subdirectory("PhysXCooking")
add_subdirectory("Common")
add_subdirectory("PxFoundation")
add_subdirectory("PxPvdSDK")
add_subdirectory("LowLevel")
add_subdirectory("LowLevelAABB")
add_subdirectory("LowLevelDynamics")
add_subdirectory("LowLevelCloth")
add_subdirectory("LowLevelParticles")
add_subdirectory("PxTask")
add_subdirectory("PsFastXml")

# # Snippets
add_subdirectory("Snippets")

# Samples
# add_subdirectory("Samples")

