# $OpenBSD: Makefile,v 1.5 2021/05/21 19:50:24 kmos Exp $

COMMENT =		backports and enhancements for the contextlib module

MODPY_EGG_VERSION =	0.5.5
DISTNAME =		contextlib2-${MODPY_EGG_VERSION}
PKGNAME =		py-contextlib2-${MODPY_EGG_VERSION}
REVISION =		2

CATEGORIES =		devel

HOMEPAGE =		http://contextlib2.readthedocs.org

MAINTAINER =		Pamela Mosiejczuk <pamela@cranky.work>

# Python-2.0
PERMIT_PACKAGE =	Yes

MODULES =		lang/python
MODPY_SETUPTOOLS =	Yes
MODPY_PI =		Yes

FLAVORS=		python3
FLAVOR?=

.if !${FLAVOR:Mpython3}
TEST_DEPENDS +=		devel/py-unittest2
.endif

.include <bsd.port.mk>
