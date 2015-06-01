COMPRESSION_LIBS = $(ZLIB_LIBS) $(XZ_LIBS) $(LZO_LIBS) $(LZ4_LIBS)

bin_PROGRAMS =
noinst_PROGRAMS =
noinst_LTLIBRARIES =
dist_man_MANS =

# Helper for FUSE clients: libfuseprivate
libfuseprivate_la_SOURCES = fuseprivate.c nonstd-makedev.c nonstd-enoattr.c \
	fuseprivate.h
libfuseprivate_la_CPPFLAGS = -I$(top_srcdir) -I$(top_srcdir)/libsquashfuse $(FUSE_CPPFLAGS)
libfuseprivate_la_LIBADD =


# High-level squashfuse
if SQ_WANT_HIGHLEVEL
bin_PROGRAMS += squashfuse
squashfuse_SOURCES = hl.c
squashfuse_CPPFLAGS = -I$(top_srcdir) -I$(top_srcdir)/libsquashfuse  $(FUSE_CPPFLAGS)
squashfuse_LDADD = $(top_builddir)/libsquashfuse/libsquashfuse.la libfuseprivate.la $(COMPRESSION_LIBS) \
  $(FUSE_LIBS)

noinst_LTLIBRARIES += libfuseprivate.la
dist_man_MANS += squashfuse.1
endif

# Low-level squashfuse_ll, if supported
if SQ_WANT_LOWLEVEL
bin_PROGRAMS += squashfuse_ll
squashfuse_ll_SOURCES = ll.c ll_inode.c nonstd-daemon.c ll.h
squashfuse_ll_CPPFLAGS = -I$(top_srcdir) -I$(top_srcdir)/libsquashfuse  $(FUSE_CPPFLAGS)
squashfuse_ll_LDADD = $(top_builddir)/libsquashfuse/libsquashfuse.la libfuseprivate.la $(COMPRESSION_LIBS) \
  $(FUSE_LIBS)

noinst_LTLIBRARIES += libfuseprivate.la
endif

if SQ_WANT_DEMO
# Sample program squashfuse_ls
noinst_PROGRAMS += squashfuse_ls
squashfuse_ls_SOURCES = ls.c
squashfuse_ls_CPPFLAGS = -I$(top_srcdir) -I$(top_srcdir)/libsquashfuse
squashfuse_ls_LDADD = $(top_builddir)/libsquashfuse/libsquashfuse.la $(COMPRESSION_LIBS)
endif
