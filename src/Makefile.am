QUIET_GEN = $(Q:@=@echo '  GEN   '$@;)

INCLUDES = \
	-DPREFIX=\"$(prefix)\" \
	-DLOCALEDIR=\"$(localedir)\" \
	-DNBTK_CACHE=\"$(pkgdatadir)/nbtk.cache\" \
	-DTHEMEDIR=\"$(pkgdatadir)/theme\"

sw-marshals.c: sw-marshals.list Makefile.am
	$(QUIET_GEN)glib-genmarshal --body --prefix=sw_marshal $< > $@

sw-marshals.h: sw-marshals.list Makefile.am
	$(QUIET_GEN)glib-genmarshal --header --prefix=sw_marshal $< > $@


libexec_PROGRAMS = meego-panel-status
lib_LTLIBRARIES = libmeego-panel-status.la

BUILT_SOURCES = sw-marshals.c sw-marshals.h

meego_panel_status_CPPFLAGS = $(STATUS_CFLAGS) $(MPL_CFLAGS) $(NM_CFLAGS)
meego_panel_status_LDADD    = $(STATUS_LIBS) $(MPL_LIBS) $(NM_LIBS) \
			      ./libmeego-panel-status.la
meego_panel_status_SOURCES  = 	\
	meego-panel-status.c


libmeego_panel_status_ladir = $(pkgincludedir)
libmeego_panel_status_la_HEADERS = \
	penge-magic-texture.h \
	penge-clickable-label.h \
	mps-tweet-card.h \
	mps-view-bridge.h \
	mps-feed-pane.h \
	mps-feed-switcher.h \
	mps-geotag-pane.h \
	sw-online.h \
	mps-module.h

libmeego_panel_status_la_SOURCES = \
	penge-magic-texture.c \
	penge-clickable-label.c \
	mps-tweet-card.c \
	mps-view-bridge.c \
	mps-feed-pane.c \
	mps-feed-switcher.c \
	mps-geotag-pane.c \
	sw-online.c \
	$(libmeego_panel_status_la_HEADERS)
libmeego_panel_status_la_CPPFLAGS = $(STATUS_CFLAGS) $(MPL_CFLAGS) $(NM_CFLAGS) \
				    -DSERVICES_MODULES_DIR=\"$(servicesdir)\"
libmeego_panel_status_la_LIBADD    = $(STATUS_LIBS) $(MPL_LIBS) $(NM_LIBS)


pkgconfig_DATA = meego-panel-status.pc
pkgconfigdir   = $(libdir)/pkgconfig

servicedir = $(datadir)/dbus-1/services
service_in_files = com.meego.UX.Shell.Panels.status.service.in
service_DATA = com.meego.UX.Shell.Panels.status.service

EXTRA_DIST = $(service_in_files) sw-marshals.list

CLEANFILES = stamp-mnb-status-marshal.h

DISTCLEANFILES = $(service_DATA) $(BUILT_SOURCES)

com.meego.UX.Shell.Panels.status.service: $(service_in_files) Makefile
	$(QUIET_GEN)sed -e "s|\@libexecdir\@|$(libexecdir)|" $< > $@
