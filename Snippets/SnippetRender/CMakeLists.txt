cmake_minimum_required(VERSION 3.8 FATAL_ERROR)

# -----------------------------------------------------------------------------------------------------------------------------
# FLAGS
# -----------------------------------------------------------------------------------------------------------------------------

if(APPLE)
    set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -DNDEBUG -DPX_SUPPORT_PVD=0 -pipe -mmacosx-version-min=10.7 -msse2 -ffast-math -fno-exceptions -fno-rtti -fvisibility=hidden -fvisibility-inlines-hidden -Werror -Wall -Wextra -fstrict-aliasing -Wstrict-aliasing=2 -pedantic -Weverything -Wno-documentation-deprecated-sync -Wno-documentation-unknown-command -Wno-float-equal -Wno-padded -Wno-weak-vtables -Wno-cast-align -Wno-conversion -Wno-missing-variable-declarations -Wno-shift-sign-overflow -Wno-global-constructors -Wno-exit-time-destructors -Wno-missing-prototypes -O3 -fno-strict-aliasing")
    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -D_DEBUG -DPX_DEBUG=1 -DPX_CHECKED=1 -DPX_SUPPORT_PVD=1 -pipe -mmacosx-version-min=10.7 -msse2 -ffast-math -fno-exceptions -fno-rtti -fvisibility=hidden -fvisibility-inlines-hidden -Werror -Wall -Wextra -fstrict-aliasing -Wstrict-aliasing=2 -pedantic -Weverything -Wno-documentation-deprecated-sync -Wno-documentation-unknown-command -Wno-float-equal -Wno-padded -Wno-weak-vtables -Wno-cast-align -Wno-conversion -Wno-missing-variable-declarations -Wno-shift-sign-overflow -Wno-global-constructors -Wno-exit-time-destructors -Wno-missing-prototypes -g3 -gdwarf-2 -O0")
elseif(WIN32)

elseif(EMSCRIPTEN)
    set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -DNDEBUG -DPX_SUPPORT_PVD=0 -pipe -msse2 -ffast-math -fno-exceptions -fno-rtti -fvisibility=hidden -fvisibility-inlines-hidden -Wno-return-type-c-linkage -Wall -Wextra -fstrict-aliasing -Wstrict-aliasing=2 -pedantic -Weverything -Wno-documentation-deprecated-sync -Wno-documentation-unknown-command -Wno-float-equal -Wno-padded -Wno-weak-vtables -Wno-cast-align -Wno-conversion -Wno-missing-variable-declarations -Wno-shift-sign-overflow -Wno-global-constructors -Wno-exit-time-destructors -Wno-missing-prototypes -O3 -fno-strict-aliasing")
    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -D_DEBUG -DPX_DEBUG=1 -DPX_CHECKED=1 -DPX_SUPPORT_PVD=1 -pipe -msse2 -ffast-math -fno-exceptions -fno-rtti -fvisibility=hidden -fvisibility-inlines-hidden -Wno-return-type-c-linkage -Wall -Wextra -fstrict-aliasing -Wstrict-aliasing=2 -pedantic -Weverything -Wno-documentation-deprecated-sync -Wno-documentation-unknown-command -Wno-float-equal -Wno-padded -Wno-weak-vtables -Wno-cast-align -Wno-conversion -Wno-missing-variable-declarations -Wno-shift-sign-overflow -Wno-global-constructors -Wno-exit-time-destructors -Wno-missing-prototypes -g3 -O0")
endif()

# -----------------------------------------------------------------------------------------------------------------------------
# FILES
# -----------------------------------------------------------------------------------------------------------------------------

# Headers
file(GLOB_RECURSE SNIPPET_RENDER_HEADERS ${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Snippets/SnippetRender/*.h)

# Sources
file(GLOB_RECURSE SNIPPET_RENDER_SOURCES ${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Snippets/SnippetRender/*.cpp)

# Source groups
source_group("Headers" FILES ${SNIPPET_RENDER_HEADERS})
source_group("Sources" FILES ${SNIPPET_RENDER_SOURCES})

# -----------------------------------------------------------------------------------------------------------------------------
# TARGETS
# -----------------------------------------------------------------------------------------------------------------------------

add_library(SnippetRender ${SNIPPET_RENDER_HEADERS} ${SNIPPET_RENDER_SOURCES})

set_target_properties(SnippetRender PROPERTIES FOLDER "Snippets")

target_include_directories(SnippetRender PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include")
target_include_directories(SnippetRender PUBLIC "${PROJECT_SOURCE_DIR}/src/PxShared/include")
target_include_directories(SnippetRender PUBLIC "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include")
target_include_directories(SnippetRender PUBLIC "${PROJECT_SOURCE_DIR}/src/PxShared/src/fastxml/include")