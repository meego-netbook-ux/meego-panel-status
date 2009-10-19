m4_define([status_version], [0.0.9])

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
                   clutter-gtk-0.10
                   mojito-client >= 0.20.1      dnl
                   telepathy-glib >= 0.9.0
                   nbtk-1.2])

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

AC_MSG_CHECKING([how to detect we are online])
AC_ARG_WITH([online],
        [AS_HELP_STRING([--with-online],
                [how to check if we are online (always, connman, networkmanager)])],
        [], [with_online=always])
AS_IF(
        [test "$with_online" = always],
        [
        AC_MSG_RESULT([always])
        AC_DEFINE([WITH_ONLINE_ALWAYS], 1, [No online detection])
        ],

        [test "$with_online" = connman],
        [
        AC_MSG_RESULT([Connection Manager])
        AC_DEFINE([WITH_ONLINE_CONNMAN], 1, [ConnMan online detection])
        ],

        [test "$with_online" = networkmanager],
        [
        AC_MSG_RESULT([Network Manager])
        PKG_CHECK_MODULES(NM, libnm_glib >= 0.7)
        AC_DEFINE([WITH_ONLINE_NM], 1, [NM online detection])
        ],

        [AC_MSG_ERROR([Unknown argument to --with-online])]
)



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
