# Initialization
AC_INIT

PACKAGE=nautilus-edit-with-vim
VERSION=0.01

AC_SUBST(PACKAGE)
AC_SUBST(VERSION)

AM_INIT_AUTOMAKE($PACKAGE, $VERSION)
AM_CONFIG_HEADER(config.h)


# Used programs

AC_PROG_CC
AM_PROG_LIBTOOL


# Check for pkg-config

AC_CHECK_PROG(HAVE_PKGCONFIG, pkg-config, yes, no)
AC_PATH_PROG(PKG_CONFIG, pkg-config, no)
if test "x$HAVE_PKGCONFIG" = "xno"; then
	AC_MSG_ERROR(you need to have pkgconfig installed !)
fi


# Dependency checks

NAUTILUS_REQUIRED=2.21.2
LIBGNOME_DESKTOP_REQUIRED=2.9.91
GLIB_REQUIRED=2.16.0

PKG_CHECK_MODULES(NAUTILUS, [
	libnautilus-extension >= $NAUTILUS_REQUIRED
	glib-2.0 >= $GLIB_REQUIRED
	gio-2.0,
	gconf-2.0
])
PKG_CHECK_MODULES(GCONF, gconf-2.0)
PKG_CHECK_MODULES(GNOMEDESKTOP, gnome-desktop-2.0 >= $LIBGNOME_DESKTOP_REQUIRED)


# Make dependency CFLAGS and LIBS available

AC_SUBST(NAUTILUS_CFLAGS)
AC_SUBST(NAUTILUS_LIBS)

AC_SUBST(GCONF_CFLAGS)
AC_SUBST(GCONF_LIBS)

AC_SUBST(GNOMEDESKTOP_CFLAGS)
AC_SUBST(GNOMEDESKTOP_LIBS)


# Get nautilus extensions directory

NAUTILUS_EXTENSION_DIR=`$PKG_CONFIG --variable=extensiondir libnautilus-extension`
AC_SUBST(NAUTILUS_EXTENSION_DIR)


# GConf

AC_PATH_PROG(GCONFTOOL, gconftool-2, no)

if test x"$GCONFTOOL" = xno; then
	AC_MSG_ERROR([gconftool-2 executable not found in your path - should be installed with GConf])
fi

AM_GCONF_SOURCE_2


# i18n

AM_GNU_GETTEXT([external])
GETTEXT_PACKAGE=nautilus-edit-with-vim
AC_SUBST([GETTEXT_PACKAGE])
AC_DEFINE_UNQUOTED([GETTEXT_PACKAGE], "$GETTEXT_PACKAGE", [Gettext package])
AM_GLIB_GNU_GETTEXT
IT_PROG_INTLTOOL([0.35.0])


# output

AC_OUTPUT([ po/Makefile.in
	Makefile 
	src/Makefile
])
