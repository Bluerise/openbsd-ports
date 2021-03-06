# $OpenBSD: Makefile,v 1.113 2021/05/10 15:08:50 tb Exp $

ONLY_FOR_ARCHS-md = aarch64 amd64 arm i386 mips64 mips64el powerpc powerpc64

COMMENT-main=	free peer-reviewed portable C++ source libraries
COMMENT-md=	machine-dependent libraries for boost

VERSION=	1.73.0
DISTNAME=	boost_${VERSION:S/./_/g}
PKGNAME-main=	boost-${VERSION}
PKGNAME-md=	boost-md-${VERSION}
CATEGORIES=	devel
MASTER_SITES=	https://boostorg.jfrog.io/artifactory/main/release/${VERSION}/source/
EXTRACT_SUFX=	.tar.bz2
FIX_EXTRACT_PERMISSIONS =	Yes
REVISION-main=	1

SO_VERSION=	14.0
BOOST_LIBS=	boost_atomic-mt \
		boost_chrono-mt boost_chrono \
		boost_container-mt boost_container \
		boost_contract-mt boost_contract \
		boost_date_time-mt boost_date_time \
		boost_filesystem-mt boost_filesystem \
		boost_graph-mt boost_graph \
		boost_iostreams-mt boost_iostreams \
		boost_locale-mt \
		boost_log-mt boost_log \
		boost_log_setup-mt boost_log_setup \
		boost_math_c99-mt boost_math_c99 \
		boost_math_c99f-mt boost_math_c99f \
		boost_math_c99l-mt boost_math_c99l \
		boost_math_tr1-mt boost_math_tr1 \
		boost_math_tr1f-mt boost_math_tr1f \
		boost_math_tr1l-mt boost_math_tr1l \
		boost_nowide-mt boost_nowide \
		boost_numpy38-mt boost_numpy38 \
		boost_prg_exec_monitor-mt boost_prg_exec_monitor \
		boost_program_options-mt boost_program_options \
		boost_python38-mt boost_python38 \
		boost_random-mt boost_random \
		boost_regex-mt boost_regex \
		boost_serialization-mt boost_serialization \
		boost_system-mt boost_system \
		boost_thread-mt \
		boost_timer-mt boost_timer \
		boost_type_erasure-mt boost_type_erasure \
		boost_unit_test_framework-mt boost_unit_test_framework \
		boost_wserialization-mt boost_wserialization \
		boost_wave-mt boost_wave

# MD
BOOST_LIBS+=	boost_context-mt \
		boost_coroutine boost_coroutine-mt \
		boost_fiber-mt \
		boost_stacktrace_basic \
		boost_stacktrace_basic-mt \
		boost_stacktrace_addr2line \
		boost_stacktrace_addr2line-mt \
		boost_stacktrace_noop \
		boost_stacktrace_noop-mt

.for _lib in ${BOOST_LIBS}
SHARED_LIBS+=	${_lib} ${SO_VERSION}
.endfor

HOMEPAGE=	https://www.boost.org/

MAINTAINER=	Brad Smith <brad@comstyle.com> \
		Rafael Sadowski <rsadowski@openbsd.org>

# Boost
PERMIT_PACKAGE=	Yes

WANTLIB += ${COMPILER_LIBCXX} bz2 icudata icui18n icuuc m z

COMPILER= base-clang ports-gcc

MULTI_PACKAGES=	-main -md

MODULES=	lang/python
MODPY_RUNDEP=	No

BUILD_DEPENDS=	math/py-numpy${MODPY_FLAVOR}

LIB_DEPENDS=	archivers/bzip2 \
		textproc/icu4c

LIB_DEPENDS-md=	devel/boost

WANTLIB-md+=	${COMPILER_LIBCXX} m boost_chrono-mt boost_filesystem-mt
WANTLIB-md+=	boost_thread-mt

.include <bsd.port.arch.mk>

.if ${PROPERTIES:Mclang}
TOOLSET=	clang
.else
TOOLSET=	gcc
.endif

BJAM_CONFIG=	-sICU_PATH=${LOCALBASE} \
		-sBZIP2_INCLUDE=${LOCALBASE}/include \
		-sBZIP2_LIBPATH=${LOCALBASE}/lib \
		-q \
		-d+2 \
		-j${MAKE_JOBS} \
		--layout=tagged-1.66 \
		pch=off \
		cflags='${CFLAGS} -pthread' \
		cxxflags='${CXXFLAGS} -pthread' \
		variant=release \
		link=static,shared \
		threading=single,multi \
		toolset=${TOOLSET}

BOOTSTRAP=	--with-bjam=${WRKSRC}/bjam \
		--with-toolset=${TOOLSET} \
		--with-python=${MODPY_BIN}

# 'context' and 'coroutine' use MD bits and miss support for Alpha,
# PA-RISC, SPARC and SuperH. The author does not care
# about adding support for Alpha and PA-RISC.
.if !${BUILD_PACKAGES:M-md}
BOOTSTRAP+=	--without-libraries=context,coroutine,fiber,stacktrace
.endif

# python.port.mk makes assumptions about an empty CONFIGURE_STYLE
CONFIGURE_STYLE= none

CONFIGURE_ENV=	BJAM_CONFIG="${BJAM_CONFIG}" \
		CXX="${CXX}" CXXFLAGS="${CXXFLAGS}"

DPB_PROPERTIES= parallel

NO_TEST=	Yes

SUBST_VARS+=	SO_VERSION

do-configure:
	echo "using ${TOOLSET} : : ${CXX} ;" >>${WRKSRC}/tools/build/src/user-config.jam
	${SUBST_CMD} ${WRKSRC}/Jamroot
	@cd ${WRKSRC}/libs/config && \
		${SETENV} ${CONFIGURE_ENV} /bin/sh ./configure
	@cd ${WRKSRC}/tools/build/src/engine && ${SETENV} ${CONFIGURE_ENV} \
		/bin/sh ./build.sh ${TOOLSET} && cp b2 bjam ${WRKSRC}
	@cd ${WRKSRC} && ${SETENV} ${CONFIGURE_ENV} /bin/sh ./bootstrap.sh ${BOOTSTRAP}

do-build:
	@cd ${WRKSRC} && export ${MAKE_ENV} && ./b2 ${BJAM_CONFIG}

do-install:
	${INSTALL_DATA_DIR} ${PREFIX}/include/boost
	${INSTALL_DATA} ${WRKSRC}/stage/lib/lib!(*.so) ${PREFIX}/lib
	cd ${WRKSRC}/boost && \
		pax -rw -s ':^.*\.orig$$::' . ${PREFIX}/include/boost
	find ${PREFIX}/include/boost -type d -exec chmod ${DIRMODE} {} +
	find ${PREFIX}/include/boost -type f -exec chmod ${SHAREMODE} {} +

.include <bsd.port.mk>
