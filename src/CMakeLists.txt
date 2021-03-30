include_directories(../include ${SKIA_ROOT})
link_directories(${SKIA_LIBPATH})

set(SOURCE
    SkottieWrapper.cpp)

add_library(SkottieWrapper SHARED ${SOURCE})

if(${CMAKE_BUILD_TYPE} STREQUAL "Debug")
  set_property(
    TARGET SkottieWrapper 
    PROPERTY MSVC_RUNTIME_LIBRARY "MultiThreadedDebug")
else()
  set_property(
    TARGET SkottieWrapper 
    PROPERTY MSVC_RUNTIME_LIBRARY "MultiThreaded")
endif()

add_compile_definitions(SKOTTIEWRAPPER_LIBRARY_BUILD)

target_link_libraries(SkottieWrapper PRIVATE
    skia.lib
    skottie.lib
    sksg.lib
    skshaper.lib
    Opengl32.lib)
