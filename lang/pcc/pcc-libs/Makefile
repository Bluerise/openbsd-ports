# $OpenBSD: Makefile,v 1.1 2021/02/18 02:26:43 daniel Exp $

COMMENT =	libraries for the portable C compiler

DISTNAME =	pcc-libs-${DISTVER}
PKGNAME =	pcc-libs-${PKGVER}

MASTER_SITES =	http://pcc.ludd.ltu.se/ftp/pub/pcc-libs/ \
		ftp://pcc.ludd.ltu.se/pub/pcc-libs/

CONFIG = 	${MACHINE_ARCH:S/amd64/x86_64/}-unknown-openbsd${OSREV}
SUBST_VARS =	CONFIG PCCVER

.include <bsd.port.mk>
