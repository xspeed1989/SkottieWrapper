set(SOURCE
    SkottieWrapper.cpp)

if(WIN32)
    enable_language(RC)
    list(APPEND SOURCE SkottieWrapper.rc)
endif()

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

if(CMAKE_SYSTEM_NAME MATCHES "Windows")
    target_link_libraries(SkottieWrapper PRIVATE
        skia
        skottie
        sksg
        skshaper
        Opengl32
    )
else()
    target_link_libraries(SkottieWrapper PRIVATE
        skia
        skottie
        sksg
        skshaper
    )
endif()

if(MSVC)
    set(_vcrt "MultiThreaded")
    if(${CMAKE_BUILD_TYPE} STREQUAL "Debug")
        set(_vcrt "MultiThreadedDebug")
    endif()
    set_target_properties(SkottieWrapper PROPERTIES MSVC_RUNTIME_LIBRARY ${_vcrt})
endif()
