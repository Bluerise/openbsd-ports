# $OpenBSD: Makefile,v 1.4 2021/03/08 13:59:25 sthen Exp $

COMMENT =	magic wormhole implementation in Go

V =		1.0.4
DISTNAME =	wormhole-william-vendored-${V}
PKGNAME =	wormhole-william-${V}
REVISION =	0

ALL_TARGET =	github.com/psanford/wormhole-william

CATEGORIES =	net
HOMEPAGE =	https://github.com/psanford/wormhole-william

MAINTAINER =	Edd Barrett <edd@openbsd.org>
# MIT
PERMIT_PACKAGE = Yes

WANTLIB += c pthread

MASTER_SITES =	https://theunixzoo.co.uk/distfiles/

MODULES =		lang/go

.include <bsd.port.mk>
