# $OpenBSD: Makefile,v 1.5 2021/05/21 19:50:25 kmos Exp $

COMMENT =	multi-producer-multi-consumer signal dispatching mechanism

MODPY_EGG_VERSION = 2.0.5
DISTNAME =	PyDispatcher-${MODPY_EGG_VERSION}
PKGNAME =	${DISTNAME:S/Py/py-/:L}
REVISION =	2

CATEGORIES =	devel

HOMEPAGE =	http://pydispatcher.sourceforge.net/

# BSD
PERMIT_PACKAGE =	Yes

MODPY_PI =	Yes
MODULES =	lang/python
MODPY_SETUPTOOLS = Yes

FLAVORS =	python3
FLAVOR ?=

.include <bsd.port.mk>
