set(SKIA_ARGS "--args=is_debug=false skia_enable_skottie=true")
if(${CMAKE_BUILD_TYPE} STREQUAL "Debug")
  set(SKIA_ARGS "--args=is_debug=true skia_enable_skottie=true")
endif()

if(CMAKE_SYSTEM_NAME MATCHES "Windows")
  string(CONCAT SKIA_ARGS "${SKIA_ARGS}" " clang_win=\"${LLVM_DIR}\"")
  message(STATUS "SKIA_ARGS:${SKIA_ARGS}")
  
  add_custom_command(
    OUTPUT Skia
    PRE_BUILD
    COMMAND ${PYTHON2_DIR}python tools/git-sync-deps
    COMMAND bin/gn gen out/Skottie  ${SKIA_ARGS}
    COMMAND ${CMAKE_CURRENT_SOURCE_DIR}/depot_tools/ninja -C out/Skottie
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/skia
    VERBATIM
    )
else()
  if(SKIA_USE_CLANG)
    string(CONCAT SKIA_ARGS "${SKIA_ARGS}" " cc=\"clang\" cxx=\"clang++\"")
  endif()
  message(STATUS "SKIA_ARGS:${SKIA_ARGS}")

  add_custom_command(
    OUTPUT Skia
    PRE_BUILD
    COMMAND python2 tools/git-sync-deps
    COMMAND bin/gn gen out/Skottie  ${SKIA_ARGS}
    COMMAND ${CMAKE_CURRENT_SOURCE_DIR}/depot_tools/ninja -C out/Skottie
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/skia
    VERBATIM
    )
endif()

add_custom_target(Build_Skia 
  DEPENDS Skia)