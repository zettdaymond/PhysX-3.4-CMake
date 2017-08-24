cmake_minimum_required(VERSION 3.8 FATAL_ERROR)

# -----------------------------------------------------------------------------------------------------------------------------
# FLAGS
# -----------------------------------------------------------------------------------------------------------------------------

if(APPLE)
    set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -DPHYSX_PROFILE_SDK -DRENDER_SNIPPET -DNDEBUG -DPX_SUPPORT_PVD=0 -pipe -mmacosx-version-min=10.7 -msse2 -ffast-math -fno-exceptions -fno-rtti -fvisibility=hidden -fvisibility-inlines-hidden -Werror -Wall -Wextra -fstrict-aliasing -Wstrict-aliasing=2 -pedantic -Weverything -Wno-documentation-deprecated-sync -Wno-documentation-unknown-command -Wno-float-equal -Wno-padded -Wno-weak-vtables -Wno-cast-align -Wno-conversion -Wno-missing-variable-declarations -Wno-shift-sign-overflow -Wno-global-constructors -Wno-exit-time-destructors -Wno-missing-prototypes -O3 -fno-strict-aliasing")
    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -DPHYSX_PROFILE_SDK -DRENDER_SNIPPET -D_DEBUG -DPX_DEBUG=1 -DPX_CHECKED=1 -DPX_SUPPORT_PVD=1 -pipe -mmacosx-version-min=10.7 -msse2 -ffast-math -fno-exceptions -fno-rtti -fvisibility=hidden -fvisibility-inlines-hidden -Werror -Wall -Wextra -fstrict-aliasing -Wstrict-aliasing=2 -pedantic -Weverything -Wno-documentation-deprecated-sync -Wno-documentation-unknown-command -Wno-float-equal -Wno-padded -Wno-weak-vtables -Wno-cast-align -Wno-conversion -Wno-missing-variable-declarations -Wno-shift-sign-overflow -Wno-global-constructors -Wno-exit-time-destructors -Wno-missing-prototypes -g3 -gdwarf-2 -O0")

    # set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -stdlib=libstdc++")
elseif(WIN32)

elseif(EMSCRIPTEN)
    set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -DPX_PHYSX_STATIC_LIB -DNDEBUG -DPX_SUPPORT_PVD=0 -pipe -msse2 -ffast-math -fno-exceptions -fno-rtti -fvisibility=hidden -fvisibility-inlines-hidden -Wall -Wextra -fstrict-aliasing -Wstrict-aliasing=2 -pedantic -Weverything -Wno-documentation-deprecated-sync -Wno-documentation-unknown-command -Wno-float-equal -Wno-padded -Wno-weak-vtables -Wno-cast-align -Wno-conversion -Wno-missing-variable-declarations -Wno-shift-sign-overflow -Wno-exit-time-destructors -Wno-global-constructors -Wno-missing-prototypes -Wno-unreachable-code -Wno-unused-macros -Wno-used-but-marked-unused -Wno-weak-template-vtables -Wno-invalid-offsetof -Wno-c++11-extensions -g3 -O3 -std=c++11 -stdlib=libc++")
    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -DPX_PHYSX_STATIC_LIB -D_DEBUG -DPX_DEBUG=1 -DPX_CHECKED=1 -DPX_SUPPORT_PVD=1 -pipe -msse2 -ffast-math -fno-exceptions -fno-rtti -fvisibility=hidden -fvisibility-inlines-hidden -Wall -Wextra -fstrict-aliasing -Wstrict-aliasing=2 -pedantic -Weverything -Wno-documentation-deprecated-sync -Wno-documentation-unknown-command -Wno-float-equal -Wno-padded -Wno-weak-vtables -Wno-cast-align -Wno-conversion -Wno-missing-variable-declarations -Wno-shift-sign-overflow -Wno-exit-time-destructors -Wno-global-constructors -Wno-missing-prototypes -Wno-unreachable-code -Wno-unused-macros -Wno-used-but-marked-unused -Wno-weak-template-vtables -Wno-invalid-offsetof -Wno-c++11-extensions -g3 -O0 -std=c++11 -stdlib=libc++")
endif()

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
elseif(WIN32)
    add_executable(SnippetHelloWorld WIN32 ${SNIPPET_HELLO_WORLD_HEADERS} ${SNIPPET_HELLO_WORLD_SOURCES})
else()
    add_executable(SnippetHelloWorld ${SNIPPET_HELLO_WORLD_HEADERS} ${SNIPPET_HELLO_WORLD_SOURCES})
endif()

set_target_properties(SnippetHelloWorld PROPERTIES FOLDER "Snippets")

target_include_directories(SnippetHelloWorld PUBLIC "${PROJECT_SOURCE_DIR}/src/PhysX_3.4/Include")
target_include_directories(SnippetHelloWorld PUBLIC "${PROJECT_SOURCE_DIR}/src/PxShared/include")
target_include_directories(SnippetHelloWorld PUBLIC "${PROJECT_SOURCE_DIR}/src/PxShared/src/foundation/include")
target_include_directories(SnippetHelloWorld PUBLIC "${PROJECT_SOURCE_DIR}/src/PxShared/src/fastxml/include")

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

# Link OS libs
if(APPLE)
    # Link Apple Frameworks
    target_link_libraries(SnippetHelloWorld "-framework OpenGL"
                                            "-framework GLUT")

    set(MACOSX_BUNDLE_BUNDLE_NAME "SnippetHelloWorld")
    set(MAC_HIGH_RESOLUTION_CAPABLE "true")
endif() 
