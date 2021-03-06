AC_INIT([osmlr],
	[unstable],
	[https://github.com/opentraffic/osmlr/issues],
	[opentraffic_osmlr-[unstable]],
	[https://github.com/opentraffic/osmlr])
AC_CONFIG_AUX_DIR([.])
AM_INIT_AUTOMAKE([subdir-objects parallel-tests])
LT_INIT
AC_SUBST([LIBTOOL_DEPS])

AM_SILENT_RULES([yes])
AC_CONFIG_HEADERS([include/config.h])
AC_CONFIG_MACRO_DIR([m4])

# set pkgconfigdir, allow override
AC_ARG_WITH([pkgconfigdir],
            AS_HELP_STRING([--with-pkgconfigdir=PATH], [Path to the pkgconfig directory [[LIBDIR/pkgconfig]]]),
            [pkgconfigdir="$withval"],
            [pkgconfigdir='${libdir}/pkgconfig'])
AC_SUBST([pkgconfigdir])

AC_PROG_CXX
AC_PROG_INSTALL
AC_PROG_MAKE_SET

AC_HEADER_STDC
AC_LANG_CPLUSPLUS

# require c++11
AX_CXX_COMPILE_STDCXX_11([noext],[mandatory])

# require other valhalla dependencies
PKG_CHECK_MODULES([VALHALLA_DEPS], [libvalhalla >= 2.3.6])

# check for protocol buffers compiler and libraries
REQUIRE_PROTOC

# check for boost and the parts we use form it
AX_BOOST_BASE([1.54], , [AC_MSG_ERROR([cannot find Boost libraries, which are are required for building tools. Please install libboost-dev.])])
AX_BOOST_PROGRAM_OPTIONS
AX_BOOST_SYSTEM
AX_BOOST_THREAD
AX_BOOST_FILESYSTEM
AX_BOOST_REGEX
AC_SUBST(BOOST_CPPFLAGS, "$BOOST_CPPFLAGS -DBOOST_SPIRIT_THREADSAFE -DBOOST_NO_CXX11_SCOPED_ENUMS")

# check pkg-config dependencies
PKG_CHECK_MODULES([DEPS], [protobuf >= 2.4.0])

# optionally enable coverage information
CHECK_COVERAGE

AC_CONFIG_FILES([Makefile])

# Debian resets this to no, but this break both Spot and the libtool
# test suite itself.  Instead of requiring developer to install a
# non-patched version of Libtool on any Debian they use, we just
# cancel the effect of Debian's patch here.
# see: http://git.lrde.epita.fr/?p=spot.git;a=commitdiff;h=0e74b76521341f670f6b76f8ef24a6dcf6e3813b
link_all_deplibs=yes
link_all_deplibs_CXX=yes

AC_OUTPUT

