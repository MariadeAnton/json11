include(${CMAKE_HOME_DIRECTORY}/biicode.cmake)
# Initializes block variables
INIT_BIICODE_BLOCK()

# Actually create targets: EXEcutables and libraries.
ADD_BIICODE_TARGETS()

# If exist BII_LIB_TARGET activate c++11 for target with PUBLIC flag. This way, all blocks that include this one will
# have activated c++11 automatically
IF(BII_LIB_TARGET)
  IF(APPLE)
    target_compile_options(${BII_LIB_TARGET} PUBLIC "-std=c++11 -stdlib=libc++")
  ELSEIF (WIN32 OR UNIX)
    target_compile_options(${BII_LIB_TARGET} PUBLIC "-std=c++11")
  ENDIF(APPLE)
# If not exist, simply add CXX_FLAGS to compilation
ELSE()
  IF(APPLE)
    SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -stdlib=libc++")
  ELSEIF (WIN32 OR UNIX)
    SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
  ENDIF(APPLE)
ENDIF()
