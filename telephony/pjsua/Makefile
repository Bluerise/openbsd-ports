# $OpenBSD: Makefile,v 1.51 2021/05/07 20:00:03 tb Exp $

COMMENT-main=	multimedia communication library (SIP, RTP, ICE, etc)
COMMENT-pjsua=	lightweight sip client

V=		2.9
REVISION=	0
DISTNAME=	pjproject-$V
PKGNAME-main=	pjsip-$V
PKGNAME-pjsua=	pjsua-$V
EXTRACT_SUFX=	.tar.bz2

LIBVER=		0.0
SHARED_LIBS +=	g7221codec                ${LIBVER}
SHARED_LIBS +=	ilbccodec                 ${LIBVER}
SHARED_LIBS +=	pj                        ${LIBVER}
SHARED_LIBS +=	pjlib-util                ${LIBVER}
SHARED_LIBS +=	pjmedia-audiodev          ${LIBVER}
SHARED_LIBS +=	pjmedia-codec             ${LIBVER}
SHARED_LIBS +=	pjmedia-videodev          ${LIBVER}
SHARED_LIBS +=	pjmedia                   ${LIBVER}
SHARED_LIBS +=	pjnath                    ${LIBVER}
SHARED_LIBS +=	pjsip-simple              ${LIBVER}
SHARED_LIBS +=	pjsip-ua                  ${LIBVER}
SHARED_LIBS +=	pjsip                     ${LIBVER}
SHARED_LIBS +=	pjsua                     ${LIBVER}
SHARED_LIBS +=	pjsua2                    ${LIBVER}
SHARED_LIBS +=	resample                  ${LIBVER}

CATEGORIES=	telephony

HOMEPAGE=	https://www.pjsip.org/
MASTER_SITES=	https://www.pjsip.org/release/$V/

# GPLv2+
PERMIT_PACKAGE=	Yes

WANTLIB += bcg729 crypto gsm m opencore-amrnb opencore-amrwb opus
WANTLIB += portaudio speex speexdsp srtp2 ssl

WANTLIB-pjsua += ${WANTLIB}
WANTLIB-pjsua += c g7221codec ilbccodec pj pjlib-util pjmedia pjmedia-audiodev
WANTLIB-pjsua += pjmedia-codec pjmedia-videodev pjnath pjsip pjsip-simple
WANTLIB-pjsua += pjsip-ua pjsua pthread resample

WANTLIB-main = ${WANTLIB} ${COMPILER_LIBCXX}

COMPILER =	base-clang ports-gcc

MULTI_PACKAGES=	-main -pjsua

LIB_DEPENDS-main= \
		audio/gsm \
		audio/opencore-amr \
		audio/opus \
		audio/portaudio-svn \
		audio/speex \
		security/libsrtp \
		telephony/bcg729

# needed for gcc archs, it's not inherited by subpackages
LIB_DEPENDS-main += ${MODGCC4_CPPLIBDEP}

LIB_DEPENDS-pjsua= telephony/pjsua,-main \
		audio/portaudio-svn

CONFIGURE_STYLE= autoconf no-autoheader
AUTOCONF_VERSION= 2.69
CONFIGURE_ARGS=	--enable-shared \
		--disable-libwebrtc \
		--disable-openh264 \
		--disable-oss \
		--disable-video \
		--with-external-gsm \
		--with-external-pa \
		--with-external-speex \
		--with-external-srtp
CFLAGS+=	-DNDEBUG -DPJ_HAS_IPV6=1 -I${LOCALBASE}/include
CONFIGURE_ENV=	LD="${CXX}" \
		CFLAGS="${CFLAGS}" \
		LDFLAGS="-L${LOCALBASE}/lib"
CONFIGURE_ENV+=	ac_cv_header_uuid_uuid_h=no \
		ac_cv_lib_uuid_uuid_generate=no

USE_GMAKE=	Yes
MAKE_FLAGS=	PJ_VERSION_MAJOR=${LIBVER} TARGET_NAME=openbsd

MODULES+=	lang/python # for tests
MODPY_VERSION =	${MODPY_DEFAULT_VERSION_2}
MODPY_BUILDDEP=	No
MODPY_RUNDEP=	No
TEST_DEPENDS=	${MODPY_RUN_DEPENDS} \
		pjsip-=$V:${BUILD_PKGPATH}
ALL_TARGET=	dep all
TEST_TARGET=	selftest

# distributed with a wrapper script that runs the real autoconf script
# in ${WRKSRC}/aconfigure; not really compatible with gnu.port.mk so
# just move it into place.
post-extract:
	mv ${WRKSRC}/aconfigure ${WRKSRC}/configure
	mv ${WRKSRC}/aconfigure.ac ${WRKSRC}/configure.ac

post-install:
	rm ${PREFIX}/lib/*.so ${PREFIX}/lib/*-openbsd.a
	${INSTALL_PROGRAM} ${WRKSRC}/pjsip-apps/bin/pjsua* ${PREFIX}/bin/pjsua

pre-test:
	ln -fs ${MODPY_BIN} ${WRKDIR}/bin/python

.include <bsd.port.mk>
