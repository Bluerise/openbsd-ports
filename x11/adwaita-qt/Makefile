# $OpenBSD: Makefile,v 1.2 2021/03/07 19:56:32 rsadowski Exp $

COMMENT =	GNOME Shell style for Qt applications

GH_ACCOUNT =	FedoraQt
GH_PROJECT =	adwaita-qt
GH_TAGNAME =	1.2.0
REVISION =	0

CATEGORIES =	x11

SHARED_LIBS +=  adwaitaqt     0.0 # 1.2
SHARED_LIBS +=  adwaitaqtpriv 0.0 # 1.2

WANTLIB += ${COMPILER_LIBCXX} Qt5Core Qt5DBus Qt5Gui Qt5Widgets
WANTLIB += Qt5X11Extras m xcb

# GPL v2 only
PERMIT_PACKAGE =	Yes

MODULES =		devel/cmake \
			x11/qt5

LIB_DEPENDS =		x11/qt5/qtx11extras


.include <bsd.port.mk>
