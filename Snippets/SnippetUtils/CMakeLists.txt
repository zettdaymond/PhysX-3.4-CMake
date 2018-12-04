# -----------------------------------------------------------------------------------------------------------------------------
# FILES
# -----------------------------------------------------------------------------------------------------------------------------

# Headers
file(GLOB_RECURSE SNIPPET_UTILS_HEADERS ${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Snippets/SnippetUtils/*.h)

# Sources
file(GLOB_RECURSE SNIPPET_UTILS_SOURCES ${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Snippets/SnippetUtils/*.cpp)

# Source groups
source_group("Headers" FILES ${SNIPPET_UTILS_HEADERS})
source_group("Sources" FILES ${SNIPPET_UTILS_SOURCES})

# -----------------------------------------------------------------------------------------------------------------------------
# TARGETS
# -----------------------------------------------------------------------------------------------------------------------------

add_library(SnippetUtils ${SNIPPET_UTILS_HEADERS} ${SNIPPET_UTILS_SOURCES})

set_target_properties(SnippetUtils PROPERTIES FOLDER "Snippets")

target_include_directories(SnippetUtils PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/Common/include")
target_include_directories(SnippetUtils PUBLIC "${PROJECT_SOURCE_DIR}/src/PxShared/include")
target_include_directories(SnippetUtils PUBLIC "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include")
target_include_directories(SnippetUtils PUBLIC "${PROJECT_SOURCE_DIR}/src/PxShared/src/fastxml/include")
target_include_directories(SnippetUtils PUBLIC "${PROJECT_SOURCE_DIR}/src/PxShared/src/pvd/include")
target_include_directories(SnippetUtils PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include")
target_include_directories(SnippetUtils PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include/utils")
target_include_directories(SnippetUtils PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Source/Common/src")
