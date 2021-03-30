LIST(APPEND CMAKE_PROGRAM_PATH  ${CMAKE_CURRENT_SOURCE_DIR}/depot_tools)

set(SKIA_ARGS "--args=is_debug=false skia_enable_skottie=true clang_win=\"${LLVM_DIR}\"")
if(${CMAKE_BUILD_TYPE} STREQUAL "Debug")
  set(SKIA_ARGS "--args=is_debug=true skia_enable_skottie=true clang_win=\"${LLVM_DIR}\"")
endif()

message(STATUS "SKIA_ARGS:${SKIA_ARGS}")

add_custom_command(
  OUTPUT Skia
  PRE_BUILD
  COMMAND ${PYTHON2_DIR}/python tools/git-sync-deps
  COMMAND bin/gn gen out/Skottie  ${SKIA_ARGS}
  COMMAND ninja -C out/Skottie
  WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/skia
  VERBATIM
  )

add_custom_target(Build_Skia 
    DEPENDS Skia)