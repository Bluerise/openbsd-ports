# $OpenBSD: Makefile,v 1.24 2021/02/26 18:20:32 naddy Exp $

COMMENT=	opensource Napster(tm) server

DISTNAME=	opennap-0.44
REVISION=	3
CATEGORIES=	audio net
MASTER_SITES=	${MASTER_SITE_SOURCEFORGE:=opennap/}

HOMEPAGE=	http://opennap.sourceforge.net/

# GPLv2
PERMIT_PACKAGE=	Yes

WANTLIB=		c z

FIX_CRLF_FILES=	metaserver.dsp

SEPARATE_BUILD=	Yes
USE_GMAKE=	Yes
CONFIGURE_STYLE=gnu
CONFIGURE_ARGS=	--enable-email \
		--enable-resume \
		--datadir=${SYSCONFDIR} \
		--with-uid=_opennap \
		--with-gid=_opennap
#		--enable-chroot \  (breaks uid, gid, and ip lookup)

DOCS=	FAQ README manual.html napster.txt

post-install:
	${INSTALL_DATA_DIR} ${PREFIX}/share/doc/opennap
	${INSTALL_DATA_DIR} ${PREFIX}/share/examples/opennap
	cd ${WRKSRC}; ${INSTALL_DATA} ${DOCS} ${PREFIX}/share/doc/opennap
	${INSTALL_DATA} ${WRKSRC}/sample.* ${PREFIX}/share/examples/opennap

.include <bsd.port.mk>
