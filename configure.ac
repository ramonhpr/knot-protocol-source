AC_PREREQ(2.60)
AC_INIT(knot-protocol, 0.01)

AM_INIT_AUTOMAKE([silent-rules subdir-objects])

AC_CONFIG_HEADERS([config.h])

m4_ifdef([AM_SILENT_RULES], [AM_SILENT_RULES([yes])])

AM_MAINTAINER_MODE

AC_PREFIX_DEFAULT(/usr/local)

PKG_PROG_PKG_CONFIG

COMPILER_WARNING_CFLAGS
COMPILER_BUILD_CFLAGS

AC_LANG_C

AC_PROG_CC
AC_PROG_CC_PIE

m4_define([_LT_AC_TAGCONFIG], [])
m4_ifdef([AC_LIBTOOL_TAGS], [AC_LIBTOOL_TAGS([])])

AM_PROG_AR
AC_PROG_RANLIB

AC_PROG_LIBTOOL

AC_ARG_ENABLE([protobuf],
	      AS_HELP_STRING([--enable-protobuf], [Enable protobuf serialization]))
if test "x$enable_protobuf" == "xyes" ; then

  PKG_CHECK_MODULES(PROTOBUF, [protobuf >= 3.0.0],
		    [AC_DEFINE([HAVE_PROTOBUF],[1],[Use PROTOBUF])],
		    [AC_MSG_ERROR("protobuf 3.0 missing")])
  AC_SUBST(PROTOBUF_CFLAGS)
  AC_SUBST(PROTOBUF_LIBS)
  PKG_CHECK_MODULES(LIBPROTOBUF_C, [libprotobuf-c],
		    [AC_DEFINE([HAVE_LIBPROTOBUF_C],[1],[Use LIBPROTOBUF_C])],
		    [AC_MSG_ERROR("libprotobuf-c missing")])
  AC_SUBST(LIBPROTOBUF_C_CFLAGS)
  AC_SUBST(LIBPROTOBUF_C_LIBS)

  AC_ARG_VAR([PROTOC], [protobuf compiler command])
  AC_PATH_PROG([PROTOC], [protoc], [],
               [`$PKG_CONFIG --variable=exec_prefix protobuf`/bin:$PATH])
  if test -z "$PROTOC"; then
    AC_MSG_ERROR([Please install the protobuf compiler from https://code.google.com/p/protobuf/.])
  fi

  PROTOBUF_VERSION="$($PROTOC --version)"
  AM_CONDITIONAL([BUILD_PROTOBUF], [test "x$enable_protobuf" == "xyes"])
else
  PROTOBUF_VERSION="not required, not building compiler"
fi

AC_CONFIG_FILES([ Makefile src/Makefile src/knotprotocol.pc])

AC_SUBST([ARFLAGS], ["cr"])

AC_OUTPUT
