# $OpenBSD: Makefile,v 1.16 2021/02/04 11:47:56 ajacoutot Exp $

COMMENT=		library for managing information about operating systems

DISTNAME=		libosinfo-${V}

SHARED_LIBS += osinfo-1.0                1.5 # 0.1009.0

WANTLIB += c gio-2.0 glib-2.0 gobject-2.0 intl soup-2.4 xml2 xslt

MODULES=		devel/meson \
			x11/gnome

MODGNOME_TOOLS=		gobject-introspection vala

BUILD_DEPENDS=		devel/gettext,-tools

# needed for test
BUILD_DEPENDS +=	devel/check

LIB_DEPENDS=		devel/libsoup \
			textproc/libxslt

RUN_DEPENDS=		misc/hwdata \
			misc/osinfo/osinfo-db

TEST_DEPENDS=		misc/osinfo/osinfo-db

CONFIGURE_ARGS=		-Dwith-pci-ids-path=${LOCALBASE}/share/hwdata/pnp.ids \
			-Dwith-usb-ids-path=${LOCALBASE}/share/hwdata/usb.ids \
			-Denable-gtk-doc=false

.include <bsd.port.mk>
