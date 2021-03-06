# Copyright (C) 2005-2009 MaNGOS project <http://getmangos.com/>
# Copyright (C) 2008-2014 TrinityCore <http://www.trinitycore.org/>
#
# This file is free software; as a special exception the author gives
# unlimited permission to copy and/or distribute it, with or without
# modifications, as long as this notice is preserved.
#
# This program is distributed in the hope that it will be useful, but
# WITHOUT ANY WARRANTY, to the extent permitted by law; without even the
# implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

file(GLOB_RECURSE sources *.cpp *.h)

set(include_Dirs
    ${CMAKE_SOURCE_DIR}/dep/libmpq
)

if( WIN32 )
  set(include_Dirs
    ${include_Dirs}
    ${CMAKE_SOURCE_DIR}/dep/libmpq/win
  )
endif()

include_directories(${include_Dirs})

add_executable(vmap4extractor ${sources})

target_link_libraries(vmap4extractor
  mpq
  ${BZIP2_LIBRARIES}
  ${ZLIB_LIBRARIES}
)

if( UNIX )
  install(TARGETS vmap4extractor DESTINATION bin)
elseif( WIN32 )
  install(TARGETS vmap4extractor DESTINATION "${CMAKE_INSTALL_PREFIX}")
endif()
