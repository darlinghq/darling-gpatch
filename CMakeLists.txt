project(gpatch)

cmake_minimum_required(VERSION 2.4.0)

if(COMMAND cmake_policy)
	cmake_policy(SET CMP0003 NEW)
	cmake_policy(SET CMP0005 NEW)
endif(COMMAND cmake_policy)

include(darling_exe)
add_definitions(-DTARGET_OS_MAC=1)
add_definitions(-D__APPLE__ -D__DYNAMIC__)
add_definitions(-DHAVE_CONFIG_H -Ded_PROGRAM="/bin/ed")

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -U_POSIX_C_SOURCE -D__DARWIN_UNIX03 -nostdinc -fPIC")
set(CMAKE_EXE_LINKER_FLAGS "-nodefaultlibs -nostdlib -Wl,--version-script=${DARLING_TOP_DIRECTORY}/darwin.map")

include_directories(${DARLING_TOP_DIRECTORY}/src/libc/include/FreeBSD)
include_directories(${DARLING_TOP_DIRECTORY}/src/libc/include/NetBSD)
include_directories(${DARLING_TOP_DIRECTORY}/src/libc/gen)
include_directories(${DARLING_TOP_DIRECTORY}/src/libc/darwin)
include_directories(${DARLING_TOP_DIRECTORY}/src/libc/stdtime/FreeBSD)
include_directories(${DARLING_TOP_DIRECTORY}/src/launchd/liblaunch)
include_directories(${DARLING_TOP_DIRECTORY}/src/external/libdispatch)
include_directories(BEFORE ${CMAKE_CURRENT_SOURCE_DIR}/patch)

set(gpatch_sources
	patch/addext.c
	patch/argmatch.c
	patch/backupfile.c
	patch/basename.c
	patch/dirname.c
	patch/error.c
	patch/exitfail.c
	patch/getopt1.c
	patch/getopt.c
	patch/inp.c
	patch/maketime.c
	patch/partime.c
	patch/patch.c
	patch/pch.c
	patch/quotearg.c
	patch/quote.c
	patch/quotesys.c
	patch/util.c
	patch/version.c
	patch/xmalloc.c
)

add_darling_executable(patch ${gpatch_sources})

install(TARGETS patch
	DESTINATION libexec/darling/usr/bin)

