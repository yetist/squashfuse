lib_LTLIBRARIES = libsquashfuse.la

INST_H_FILES =		\
	cache.h		\
	common.h	\
	decompress.h	\
	dir.h		\
	file.h		\
	fs.h		\
	squashfs_fs.h	\
	squashfuse.h	\
	stack.h		\
	table.h		\
	traverse.h	\
	util.h		\
	xattr.h

NOINST_H_FILES = 	\
	nonstd-internal.h \
	nonstd.h	\
	swap.h		\
	squashfuse.h	\
	hash.h

# Main library: libsquashfuse
libsquashfuse_la_SOURCES = \
	cache.c \
	decompress.c \
	dir.c \
	file.c \
	fs.c \
	hash.c \
	nonstd-pread.c \
	nonstd-stat.c \
	stack.c \
	swap.c \
	table.c \
	traverse.c \
	util.c \
	xattr.c \
	$(INST_H_FILES) \
	$(NOINST_H_FILES)
	
libsquashfuse_la_CPPFLAGS = \
	-I$(top_srcdir)			\
	-I$(top_srcdir)/libsquashfuse	\
	$(ZLIB_CPPFLAGS) \
       	$(XZ_CPPFLAGS) \
       	$(LZO_CPPFLAGS) \
	$(LZ4_CPPFLAGS)

libsquashfuse_la_LIBADD =

$(libsquashfuse_la_OBJECTS): swap.h.inc swap.c.inc

swap.h.inc: squashfs_fs.h Makefile
	$(AM_V_GEN) $(SED) -n '/^struct squashfs_/{s/^struct \(squashfs_\([^[:space:]]*\)\).*/void sqfs_swapin_\2(struct \1 *s);\n/p}' $^ > $@

swap.c.inc: squashfs_fs.h Makefile
	$(AM_V_GEN) $(SED) -n -e '/^struct squashfs_/,/^}/{s/^struct \(squashfs_\([^[:space:]]*\)\).*/void sqfs_swapin_\2(struct \1 *s){/p; s/^};/}\n/p}' \
		-e 's/^[[:space:]]*__le\([[:digit:]]*\)[[:space:]]*\([a-z_]*\);$$/\tsqfs_swapin\1_internal(\&s->\2);/p' $^ > $@

install_headerdir = $(prefix)/include/libsquashfuse
install_header_HEADERS = $(INST_H_FILES)

# Handle generation of swap include files
CLEANFILES =		\
	swap.h.inc	\
	swap.c.inc

EXTRA_DIST =		\
	swap.h.inc	\
	swap.c.inc
