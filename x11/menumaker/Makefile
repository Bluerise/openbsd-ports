# $OpenBSD: Makefile,v 1.8 2021/02/23 19:39:52 sthen Exp $

COMMENT =	menu generation utility for X window managers
DISTNAME =	menumaker-0.99.12
CATEGORIES =	x11

MASTER_SITES =	${MASTER_SITE_SOURCEFORGE:=menumaker/}

HOMEPAGE =	http://menumaker.sourceforge.net/
MAINTAINER =	Alessandro De Laurenzis <just22@atlantide.mooo.com>

# BSD
PERMIT_PACKAGE = Yes

MODULES =	lang/python

CONFIGURE_STYLE = gnu

MAKE_FLAGS =	PYTHON=${MODPY_BIN}

NO_TEST =	Yes

post-install:
	${MODPY_BIN} ${MODPY_LIBDIR}/compileall.py \
	    ${PREFIX}/share/menumaker

.include <bsd.port.mk>
