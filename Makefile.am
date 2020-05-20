AM_MAKEFLAGS = --no-print-directory

AM_CFLAGS = $(WARNING_CFLAGS) $(BUILD_CFLAGS)
AM_LDFLAGS = $(BUILD_LDFLAGS)
BUILT_SOURCES = 

SUBDIRS = src
dist_doc_DATA = README

if BUILD_PROTOBUF
src/knot.pb-c.c src/knot.pb-c.h: 
	$(AM_V_GEN)@PROTOC@ -I$(top_srcdir) --c_out=$(top_builddir) $(top_builddir)/src/knot.proto

src/knot_pb3.py: 
	$(AM_V_GEN)@PROTOC@ -I$(top_srcdir) --python_out=$(top_builddir) $(top_builddir)/src/knot.proto

BUILT_SOURCES += \
	src/knot.pb-c.c src/knot.pb-c.h
endif

MAINTAINERCLEANFILES = Makefile.in \
	aclocal.m4 configure config.h.in config.sub config.guess \
	ltmain.sh depcomp compile missing install-sh

if BUILD_PROTOBUF
CLEANFILES = $(BUILT_SOURCES)
MAINTAINERCLEANFILES += $(BUILT_SOURCES)
endif
