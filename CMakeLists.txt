project( libmfx )

find_path ( INTELMEDIASDK_PATH include/mfxvideo.h
  HINTS "${CMAKE_SOURCE_DIR}/sdk/" "$ENV{HOME}/.wine/drive_c/Program Files (x86)/Intel/Media SDK 2013/"
  ENV INTELMEDIASDK_PATH
  NO_DEFAULT_PATH)

if (INTELMEDIASDK_PATH)
  message("Intel Media SDK include folder found ! (${INTELMEDIASDK_PATH})")
else (INTELMEDIASDK_PATH)
  message(FATAL_ERROR "Intel Media SDK include folder required, but not found !")
endif (INTELMEDIASDK_PATH)

set(SOURCES
  src/main.cpp
  src/mfx_critical_section.cpp
  src/mfx_dispatcher.cpp
  src/mfx_dispatcher_log.cpp
  src/mfx_dxva2_device.cpp
  src/mfx_function_table.cpp
  src/mfx_library_iterator.cpp
  src/mfx_load_dll.cpp
  src/mfx_win_reg_key.cpp
)

include_directories(
  ${INTELMEDIASDK_PATH}/include
  include
)

add_definitions(
  -DMFX_VA
  -DWIN32
  -D_DEBUG
  -D_LIB
)

add_library( libmfx STATIC ${SOURCES} )
cmake_minimum_required(VERSION 2.6)
