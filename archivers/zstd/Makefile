# $OpenBSD: Makefile,v 1.36 2021/03/06 19:31:22 bket Exp $

COMMENT =		zstandard fast real-time compression algorithm

V =			1.4.9
DISTNAME =		zstd-${V}

SHARED_LIBS =		zstd	5.0	# 1.4.9

CATEGORIES =		archivers

HOMEPAGE =		https://facebook.github.io/zstd/

MAINTAINER =		Bjorn Ketelaars <bket@openbsd.org>

# BSD 3 clauses + GPLv2
PERMIT_PACKAGE =	Yes

WANTLIB =		c lz4 lzma pthread z

MASTER_SITES =		https://github.com/facebook/zstd/releases/download/v${V}/

LIB_DEPENDS =		archivers/lz4 \
			archivers/xz
BUILD_DEPENDS =		sysutils/ggrep

MAKE_ENV =		CC="${CC}" \
			CPPFLAGS="-I${LOCALBASE}/include" \
			LDFLAGS="${LDFLAGS} -L${LOCALBASE}/lib"
MAKE_FLAGS =		SHARED_EXT_VER="so.$(LIBzstd_VERSION)" \
			SONAME_FLAGS= \
			V=1
FAKE_FLAGS =		PREFIX="${PREFIX}"

USE_GMAKE =		Yes

DEBUG_PACKAGES =	${BUILD_PACKAGES}

ALL_TARGET =		default
TEST_TARGET =		check

pre-build:
	ln -fs ${LOCALBASE}/bin/ggrep ${WRKDIR}/bin/grep

.include <bsd.port.mk>
