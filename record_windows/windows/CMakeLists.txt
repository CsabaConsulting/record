# The Flutter tooling requires that developers have a version of Visual Studio
# installed that includes CMake 3.14 or later. You should not increase this
# version, as doing so will cause the plugin to fail to compile for some
# customers of the plugin.
cmake_minimum_required(VERSION 3.14)

# Project-level configuration.
set(PROJECT_NAME "record_windows")
project(${PROJECT_NAME} LANGUAGES CXX)

# This value is used when generating builds using this plugin, so it must
# not be changed
set(PLUGIN_NAME "record_windows_plugin")

# Any new source files that you add to the plugin should be added here.
list(APPEND PLUGIN_SOURCES
  "record_windows_plugin.cpp"
  "record_windows_plugin.h"
)

# Define the plugin library target. Its name must not be changed (see comment
# on PLUGIN_NAME above).
add_library(${PLUGIN_NAME} SHARED
  "include/record_windows/record_windows_plugin_c_api.h"
  "record_windows_plugin_c_api.cpp"
  ${PLUGIN_SOURCES}
)

# Apply a standard set of build settings that are configured in the
# application-level CMakeLists.txt. This can be removed for plugins that want
# full control over build settings.
apply_standard_settings(${PLUGIN_NAME})

# Symbols are hidden by default to reduce the chance of accidental conflicts
# between plugins. This should not be removed; any symbols that should be
# exported should be explicitly exported with the FLUTTER_PLUGIN_EXPORT macro.
set_target_properties(${PLUGIN_NAME} PROPERTIES
  CXX_VISIBILITY_PRESET hidden)
target_compile_definitions(${PLUGIN_NAME} PRIVATE FLUTTER_PLUGIN_IMPL)

# Source include directories and library dependencies. Add any plugin-specific
# dependencies here.
target_include_directories(${PLUGIN_NAME} INTERFACE
  "${CMAKE_CURRENT_SOURCE_DIR}/include")
target_link_libraries(${PLUGIN_NAME} PRIVATE flutter flutter_wrapper_plugin)

# List of absolute paths to libraries that should be bundled with the plugin.
# This list could contain prebuilt libraries, or libraries created by an
# external build triggered from this build file.
set(record_windows_bundled_libraries
  ""
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/fmedia.exe"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/fmedia.conf"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/aac.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/afilter.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/alac.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/ape.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/core.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/direct-sound.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/dynanorm.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/flac.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/fmt.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libALAC-ff.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libDynamicAudioNormalizer-ff.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libfdk-aac-ff.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libFLAC-ff.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libMAC-ff.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libmp3lame-ff.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libmpc-ff.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libmpg123-ff.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libogg-ff.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libopus-ff.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libsoxr-ff.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libvorbis-ff.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libvorbisenc-ff.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libwavpack-ff.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/mpc.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/mpeg.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/net.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/opus.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/plist.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/soxr.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/tui.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/vorbis.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/wasapi.dll"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/wavpack.dll"
  PARENT_SCOPE
)