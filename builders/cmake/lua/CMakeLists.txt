cmake_minimum_required(VERSION 2.6)
PROJECT(lua)


IF(CMAKE_SYSTEM_NAME MATCHES "FreeBSD" OR CMAKE_SYSTEM_NAME MATCHES "OpenBSD")
    ADD_DEFINITIONS(-DLUA_USE_LINUX)
ELSEIF(CMAKE_SYSTEM_NAME MATCHES "Darwin")
    ADD_DEFINITIONS(-DLUA_USE_LINUX)
ELSEIF(CMAKE_SYSTEM_NAME MATCHES "Linux")
    ADD_DEFINITIONS(-DLUA_USE_LINUX)
ELSEIF(CMAKE_SYSTEM_NAME MATCHES "SunOS")
    ADD_DEFINITIONS(-DLUA_USE_POSIX)
    ADD_DEFINITIONS(-DLUA_USE_DLOPEN)
ELSE(CMAKE_SYSTEM_NAME MATCHES "FreeBSD")
    MESSAGE(FATAL_ERROR "Platform ${CMAKE_SYSTEM_NAME} not supported yet")
ENDIF(CMAKE_SYSTEM_NAME MATCHES "FreeBSD" OR CMAKE_SYSTEM_NAME MATCHES "OpenBSD")


#make the list with all the source files
FILE(GLOB_RECURSE SOURCES "${CRTMPSERVER_3RDPARTY_ROOT}/lua-dev/*.c" )

#prepare the include directories
INCLUDE_DIRECTORIES(
	${LUA_INCLUDE_PATH}
)

#create THE library
ADD_LIBRARY(lua SHARED ${SOURCES})
INSTALL(TARGETS ${PROJECT_NAME} LIBRARY DESTINATION ${CRTMPSERVER_ROOT})

