# $OpenBSD: Makefile,v 1.5 2021/02/14 14:24:20 sthen Exp $

COMMENT=	sip module support for PyQt5

MODPY_EGG_VERSION=	12.8.1

DISTNAME=	PyQt5_sip-${MODPY_EGG_VERSION}
PKGNAME=	py-${DISTNAME:L}

CATEGORIES=	x11

HOMEPAGE=	https://www.riverbankcomputing.com/software/sip/

# SIP license (Python-like) or GPLv2/v3
PERMIT_PACKAGE=	Yes

MODULES=	lang/python
FLAVOR=		python3
FLAVORS=	python3

MODPY_PI=	Yes
MODPY_SETUPTOOLS= Yes

NO_TEST=	Yes

RUN_DEPENDS=	devel/py-sip${MODPY_FLAVOR}

.include <bsd.port.mk>
