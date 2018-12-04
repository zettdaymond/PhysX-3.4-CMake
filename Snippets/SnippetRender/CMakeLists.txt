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

if(WIN32)
    target_include_directories(SnippetRender PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Snippets/Graphics/include/win32/GL")
endif()
