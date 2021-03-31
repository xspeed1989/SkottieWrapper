set(SOURCE
    SkottieWrapper.cpp)

add_library(SkottieWrapper SHARED ${SOURCE})

target_include_directories(SkottieWrapper PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/../include
    ${SKIA_ROOT}
)

target_link_directories(SkottieWrapper PRIVATE
    ${SKIA_LIBPATH}
)

target_compile_definitions(SkottieWrapper PRIVATE
    SKOTTIEWRAPPER_LIBRARY_BUILD
)

target_link_libraries(SkottieWrapper PRIVATE
    skia
    skottie
    sksg
    skshaper
    Opengl32
)

if(MSVC)
    set(_vcrt "MultiThreaded")
    if(${CMAKE_BUILD_TYPE} STREQUAL "Debug")
        set(_vcrt "MultiThreadedDebug")
    endif()
    set_target_properties(SkottieWrapper PROPERTIES MSVC_RUNTIME_LIBRARY ${_vcrt})
endif()
