# -----------------------------------------------------------------------------------------------------------------------------
# FILES
# -----------------------------------------------------------------------------------------------------------------------------

# Headers
file(GLOB_RECURSE PXFOUNDATION_HEADERS ${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include/*.h ${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/src/*.h)

# Sources
file(GLOB_RECURSE PXFOUNDATION_SOURCES ${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/*.cpp)

if(WIN32)
    list(REMOVE_ITEM PXFOUNDATION_HEADERS
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include/unix/neon/PsUnixNeonAoS.h"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include/unix/neon/PsUnixNeonInlineAoS.h"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include/unix/PsUnixAoS.h"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include/unix/PsUnixFPU.h"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include/unix/PsUnixInlineAoS.h"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include/unix/PsUnixIntrinsics.h"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include/unix/PsUnixTrigConstants.h")

    list(REMOVE_ITEM PXFOUNDATION_SOURCES
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/src/unix/PsUnixAtomic.cpp"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/src/unix/PsUnixCpu.cpp"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/src/unix/PsUnixFPU.cpp"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/src/unix/PsUnixMutex.cpp"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/src/unix/PsUnixPrintString.cpp"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/src/unix/PsUnixSList.cpp"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/src/unix/PsUnixSocket.cpp"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/src/unix/PsUnixSync.cpp"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/src/unix/PsUnixThread.cpp"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/src/unix/PsUnixTime.cpp")
else()
    list(REMOVE_ITEM PXFOUNDATION_HEADERS
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include/windows/PsWindowsAoS.h"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include/windows/PsWindowsFPU.h"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include/windows/PsWindowsInclude.h"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include/windows/PsWindowsInlineAoS.h"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include/windows/PsWindowsLoadLibrary.h"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include/windows/PsWindowsIntrinsics.h"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include/windows/PsWindowsTrigConstants.h"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include/unix/neon/PsUnixNeonAoS.h"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include/unix/neon/PsUnixNeonInlineAoS.h")
    list(REMOVE_ITEM PXFOUNDATION_SOURCES
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/src/windows/PsWindowsAtomic.cpp"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/src/windows/PsWindowsCpu.cpp"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/src/windows/PsWindowsFPU.cpp"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/src/windows/PsWindowsMutex.cpp"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/src/windows/PsWindowsPrintString.cpp"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/src/windows/PsWindowsSList.cpp"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/src/windows/PsWindowsSocket.cpp"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/src/windows/PsWindowsSync.cpp"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/src/windows/PsWindowsThread.cpp"
        "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/src/windows/PsWindowsTime.cpp")
endif()

# Source groups
source_group("Headers" FILES ${PXFOUNDATION_HEADERS})
source_group("Sources" FILES ${PXFOUNDATION_SOURCES})

# -----------------------------------------------------------------------------------------------------------------------------
# TARGETS
# -----------------------------------------------------------------------------------------------------------------------------

add_library(PxFoundation STATIC STATIC ${PXFOUNDATION_HEADERS} ${PXFOUNDATION_SOURCES})

set_target_properties(PxFoundation PROPERTIES FOLDER "PhysX")
if (UNIX AND NOT ANDROID)
    target_link_libraries(PxFoundation pthread)
endif ()

target_include_directories(PxFoundation PUBLIC "${PROJECT_SOURCE_DIR}/src/PxShared/include")
target_include_directories(PxFoundation PUBLIC "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include")
