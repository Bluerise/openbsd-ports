# $OpenBSD: Makefile,v 1.12 2021/03/14 19:50:49 bket Exp $

COMMENT-main =		mail indexer, tagger and threader
COMMENT-emacs =		Emacs bindings for notmuch

PKGNAME-main =		notmuch-${V}
PKGNAME-emacs =		notmuch-emacs-${V}

SHARED_LIBS +=		notmuch	1.0

MULTI_PACKAGES =	-main -emacs
DEBUG_PACKAGES =	-main

COMPILER=		base-clang ports-gcc

WANTLIB-main +=		${COMPILER_LIBCXX} c glib-2.0 gmime-3.0 gobject-2.0
WANTLIB-main +=		talloc xapian z

LIB_DEPENDS =		databases/xapian-core \
			devel/libtalloc \
			mail/gmime30

RUN_DEPENDS-emacs =	devel/desktop-file-utils \
			databases/xapian-core \
			editors/emacs \
			${FULLPKGNAME-main}:${FULLPKGPATH-main}

BUILD_DEPENDS =		devel/doxygen \
			devel/py-cffi${MODPY_FLAVOR} \
			editors/emacs,gtk3 \
			security/gnupg>=2.2.23p1 \
			shells/bash \
			shells/bash-completion \
			textproc/py-sphinx${MODPY_FLAVOR}

TEST_DEPENDS =		archivers/gtar \
			devel/gdb \
			misc/dtach \
			sysutils/coreutils \
			${FULLPKGNAME-main}:${FULLPKGPATH-main}

MODULES =		lang/python
MODPY_RUNDEP =		No
MODPY_PYTEST =		Yes
USE_GMAKE =		Yes
CONFIGURE_STYLE =	simple
CONFIGURE_ARGS =	--mandir=${PREFIX}/man \
			--infodir=${PREFIX}/info \
			--sysconfdir=${SYSCONFDIR} \
			--bashcompletiondir=${PREFIX}/share/notmuch/bash_completion.d
CONFIGURE_ENV =		PYTHON=${MODPY_BIN}
MAKE_FLAGS =		V=1
MAKE_ENV =		LIBnotmuch_MAJOR=${LIBnotmuch_VERSION:R} \
			LIBnotmuch_MINOR=${LIBnotmuch_VERSION:E}

# the --gzip option of notmuch dump is disabled so skip the relevant tests
TEST_FLAGS =	V=1 \
		NOTMUCH_TEST_SERIALIZE=1 \
		NOTMUCH_SKIP_TESTS="dump-restore.14 dump-restore.15" \
		TEST_CFLAGS="-O0 -g -I${LOCALBASE}/include -L${LOCALBASE}/lib"
TEST_TARGET =	test

post-extract:
	cd ${WRKSRC}/test; [ -r test-lib-OPENBSD.sh ] || \
	    cp test-lib-FREEBSD.sh test-lib-OPENBSD.sh

post-install:
	rm ${PREFIX}/man/man1/notmuch-setup.1.gz
	gunzip ${PREFIX}/man/*/*gz
	ln -s notmuch.1 ${PREFIX}/man/man1/notmuch-setup.1

.include <bsd.port.mk>
