# -----------------------------------------------------------------------------------------------------------------------------
# FILES
# -----------------------------------------------------------------------------------------------------------------------------

# Headers
file(GLOB_RECURSE SNIPPET_HELLO_WORLD_HEADERS ${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Snippets/SnippetHelloWorld/*.h)

# Sources
file(GLOB_RECURSE SNIPPET_HELLO_WORLD_SOURCES ${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Snippets/SnippetHelloWorld/*.cpp)
list(APPEND SNIPPET_HELLO_WORLD_SOURCES ${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Snippets/SnippetCommon/ClassicMain.cpp)

# Source groups
source_group("Headers" FILES ${SNIPPET_HELLO_WORLD_HEADERS})
source_group("Sources" FILES ${SNIPPET_HELLO_WORLD_SOURCES})

# -----------------------------------------------------------------------------------------------------------------------------
# TARGETS
# -----------------------------------------------------------------------------------------------------------------------------

if(APPLE)
    add_executable(SnippetHelloWorld MACOSX_BUNDLE ${SNIPPET_HELLO_WORLD_HEADERS} ${SNIPPET_HELLO_WORLD_SOURCES})
else()
    add_executable(SnippetHelloWorld ${SNIPPET_HELLO_WORLD_HEADERS} ${SNIPPET_HELLO_WORLD_SOURCES})
endif()

set_target_properties(SnippetHelloWorld PROPERTIES FOLDER "Snippets")

target_include_directories(SnippetHelloWorld PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include")
target_include_directories(SnippetHelloWorld PUBLIC "${PROJECT_SOURCE_DIR}/src/PxShared/include")
target_include_directories(SnippetHelloWorld PUBLIC "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include")
target_include_directories(SnippetHelloWorld PUBLIC "${PROJECT_SOURCE_DIR}/src/PxShared/src/fastxml/include")

if(WIN32)
    target_include_directories(SnippetHelloWorld PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Snippets/Graphics/include/win32/GL")
endif()

# -----------------------------------------------------------------------------------------------------------------------------
# LINKING
# -----------------------------------------------------------------------------------------------------------------------------

# Link PhysX3 libs
target_link_libraries(SnippetHelloWorld PhysX3Common)
target_link_libraries(SnippetHelloWorld PhysX3)
target_link_libraries(SnippetHelloWorld PhysX3Vehicle)
target_link_libraries(SnippetHelloWorld PhysX3Cooking)
target_link_libraries(SnippetHelloWorld PhysX3Extensions)
target_link_libraries(SnippetHelloWorld PhysX3CharacterKinematic)
target_link_libraries(SnippetHelloWorld PxFoundation)
target_link_libraries(SnippetHelloWorld PsFastXml)
target_link_libraries(SnippetHelloWorld PxPvdSDK)
target_link_libraries(SnippetHelloWorld SimulationController)
target_link_libraries(SnippetHelloWorld SceneQuery)
target_link_libraries(SnippetHelloWorld LowLevel)
target_link_libraries(SnippetHelloWorld LowLevelAABB)
target_link_libraries(SnippetHelloWorld LowLevelDynamics)
target_link_libraries(SnippetHelloWorld LowLevelCloth)
target_link_libraries(SnippetHelloWorld LowLevelParticles)
target_link_libraries(SnippetHelloWorld PxTask)

# Link Snippet libs
target_link_libraries(SnippetHelloWorld SnippetUtils)
target_link_libraries(SnippetHelloWorld SnippetRender)

if(WIN32)
    target_link_libraries(SnippetHelloWorld "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Snippets/Graphics/lib/win64/glut/glut32.lib")
endif()

# Link OS libs
if(APPLE)
    # Link Apple Frameworks
    target_link_libraries(SnippetHelloWorld "-framework OpenGL"
                                            "-framework GLUT")

    set(MACOSX_BUNDLE_BUNDLE_NAME "SnippetHelloWorld")
    set(MAC_HIGH_RESOLUTION_CAPABLE "true")
endif() 

if(EMSCRIPTEN)
    set(LINK_LIBS PhysX3Common PhysX3 PhysX3Vehicle PhysX3Cooking PhysX3Extensions PhysX3CharacterKinematic PxFoundation PsFastXml PxPvdSDK SimulationController SceneQuery LowLevel LowLevelAABB LowLevelDynamics LowLevelCloth LowLevelParticles PxTask)
    target_link_libraries(SnippetHelloWorld ${LINK_LIBS} ${LINK_LIBS})
    set_target_properties(SnippetHelloWorld PROPERTIES LINK_FLAGS "-s LEGACY_GL_EMULATION=1 -o main.html --std=c++11")
endif()
