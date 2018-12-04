# -----------------------------------------------------------------------------------------------------------------------------
# FILES
# -----------------------------------------------------------------------------------------------------------------------------

# Headers
file(GLOB_RECURSE PXPVDSDK_HEADERS ${PROJECT_SOURCE_DIR}/src/PxShared/include/pvd/*.h ${PROJECT_SOURCE_DIR}/src/PxShared/src/pvd/include/*.h ${PROJECT_SOURCE_DIR}/src/PxShared/src/pvd/src/*.h)

# Sources
file(GLOB_RECURSE PXPVDSDK_SOURCES ${PROJECT_SOURCE_DIR}/src/PxShared/src/pvd/src/*.cpp)

if(UNIX OR APPLE)
    list(REMOVE_ITEM PXPVDSDK_HEADERS "${PROJECT_SOURCE_DIR}/src/PxShared/include/pvd/windows/PxWindowsPvdDelayLoadHook.h")
    list(REMOVE_ITEM PXPVDSDK_SOURCES "${PROJECT_SOURCE_DIR}/src/PxShared/src/pvd/src/windows/PxWindowsPvdDelayLoadHook.cpp")
endif()

# Source groups
source_group("Headers" FILES ${PXPVDSDK_HEADERS})
source_group("Sources" FILES ${PXPVDSDK_SOURCES})

# -----------------------------------------------------------------------------------------------------------------------------
# TARGETS
# -----------------------------------------------------------------------------------------------------------------------------

add_library(PxPvdSDK STATIC ${PXPVDSDK_HEADERS} ${PXPVDSDK_SOURCES})
if(WIN32)
    target_link_libraries(PxPvdSDK "${PROJECT_SOURCE_DIR}/src/Externals/nvToolsExt/1/lib/x64/nvToolsExt64_1.lib")
endif()
set_target_properties(PxPvdSDK PROPERTIES FOLDER "PhysX")
target_link_libraries(PxPvdSDK PxFoundation)

target_include_directories(PxPvdSDK PUBLIC "${PROJECT_SOURCE_DIR}/src/PxShared/include")
target_include_directories(PxPvdSDK PUBLIC "${PROJECT_SOURCE_DIR}/src/PxShared/src/pvd/include")
target_include_directories(PxPvdSDK PUBLIC "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include")
target_include_directories(PxPvdSDK PUBLIC "${PROJECT_SOURCE_DIR}/src/PxShared/src/filebuf/include")
target_include_directories(PxPvdSDK PUBLIC "${PROJECT_SOURCE_DIR}/src/Externals/nvToolsExt/1/include")
