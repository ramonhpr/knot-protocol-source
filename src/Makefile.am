lib_headers = knot_protocol.h knot_types.h
lib_sources = knot_protocol.c

libknotprotocol_includedir = $(includedir)/knot
libknotprotocol_include_HEADERS = $(lib_headers)

lib_LTLIBRARIES = libknotprotocol.la
libknotprotocol_la_SOURCES = $(lib_headers) $(lib_sources)
libknotprotocol_la_LDFLAGS = $(AM_LDFLAGS)

pkgconfigdir = $(libdir)/pkgconfig

pkgconfig_DATA = knotprotocol.pc

if BUILD_PROTOBUF
noinst_LTLIBRARIES = libknotprotobuf.la
libknotprotobuf_la_SOURCES = knot.pb-c.c knot.pb-c.h
libknotprotobuf_la_LDFLAGS = $(AM_LDFLAGS) @PROTOBUF_LIBS@ @LIBPROTOBUF_C_LIBS@
libknotprotobuf_la_CFLAGS  = $(AM_CFLAGS)  @PROTOBUF_CFLAGS@ @LIBPROTOBUF_C_CFLAGS@
libknotprotocol_include_HEADERS += knot.pb-c.h
libknotprotocol_la_LIBADD = libknotprotobuf.la
endif

MAINTAINERCLEANFILES = Makefile.in libknotprotobuf.la libknotprotocol.la
