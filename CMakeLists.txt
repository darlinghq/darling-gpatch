project(gpatch)

cmake_minimum_required(VERSION 2.4.0)

if(COMMAND cmake_policy)
	cmake_policy(SET CMP0003 NEW)
	cmake_policy(SET CMP0005 NEW)
endif(COMMAND cmake_policy)

add_compile_definitions(
	HAVE_CONFIG_H
	ed_PROGRAM="/bin/ed"

	__DARWIN_UNIX03
)

# Hide warnings
add_compile_options(
	-Wno-string-plus-int
	-Wno-format-security
	-Wno-macro-redefined
	-Wno-constant-logical-operand
)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -nostdinc -fPIC")

include_directories(BEFORE
	${CMAKE_CURRENT_SOURCE_DIR}/gen
	${CMAKE_CURRENT_SOURCE_DIR}/patch
)

add_darling_executable(patch
	patch/addext.c
	patch/argmatch.c
	patch/backupfile.c
	patch/basename.c
	patch/dirname.c
	patch/error.c
	patch/exitfail.c
	patch/getopt.c
	patch/getopt1.c
	patch/inp.c
	patch/maketime.c
	patch/partime.c
	patch/patch.c
	patch/pch.c
	patch/quote.c
	patch/quotearg.c
	patch/quotesys.c
	patch/util.c
	patch/version.c
	patch/xmalloc.c
)

install(TARGETS patch DESTINATION libexec/darling/usr/bin)
install(FILES patch/patch.man DESTINATION libexec/darling/usr/share/man/man1 RENAME patch.1)
