m4_define([status_version], [0.0.4])

AC_PREREQ([2.59])
AC_INIT([moblin-panel-status], [status_version])

AM_INIT_AUTOMAKE([AC_PACKAGE_NAME], [AC_PACKAGE_VERSION])
AM_CONFIG_HEADER([config.h])

AC_CANONICAL_HOST
AC_PROG_CC
AC_PROG_CC_STDC
AC_PROG_INSTALL
AC_PROG_LIBTOOL
AC_ISC_POSIX
AC_HEADER_STDC

AM_PROG_CC_C_O
AM_PATH_GLIB_2_0

PKG_CHECK_MODULES([MPL], [moblin-panel])
PKG_CHECK_MODULES([STATUS],
                  [dbus-glib-1                  dnl
                   clutter-x11-1.0 >= 1.0.0     dnl
                   libmissioncontrol            dnl
                   mojito-client >= 0.20        dnl
                   nbtk-1.0])

AC_ARG_ENABLE([cache],
              [AC_HELP_STRING([--enable-cache],
                              [Enable Nbtk image cache generation])],
              [],
              [enable_cache=no])

AS_IF([test "x$enable_cache" = "xyes"],
      [
        AC_CHECK_PROG([NBTK_CREATE_IMAGE_CACHE],
                      [nbtk-create-image-cache],
                      [$(which nbtk-create-image-cache)])
      ]
)

AM_CONDITIONAL([ENABLE_CACHE], [test "x$enable_cache" = "xyes"])

IT_PROG_INTLTOOL([0.35.0])
GETTEXT_PACKAGE=moblin-panel-status
AC_SUBST(GETTEXT_PACKAGE)
AC_DEFINE_UNQUOTED([GETTEXT_PACKAGE],
                   ["$GETTEXT_PACKAGE"],
                   [Gettext domain name])
AM_GLIB_GNU_GETTEXT

AC_OUTPUT([
        Makefile
        src/Makefile
        data/Makefile
        data/theme/Makefile
        po/Makefile.in
])
