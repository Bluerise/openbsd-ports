# $OpenBSD: Makefile,v 1.54 2021/04/09 17:41:15 florian Exp $

COMMENT =	next-generation web UI for icinga

GH_ACCOUNT =	Icinga
GH_PROJECT =	icingaweb2
GH_TAGNAME =	v2.8.2
REVISION =	8
PKGNAME =	icinga-web2-${GH_TAGNAME:S/v//}

MAINTAINER =	Stuart Henderson <stu.ports@spacehopper.org>
MODULES=	lang/php

MODPHP_PDO_ALLOWED = mysql pgsql
MODPHP_PDO_PREF =    mysql

RUN_DEPENDS =	lang/php/${MODPHP_VERSION},-intl \
		${MODPHP_PDO_DEPENDS}

NO_TEST =	Yes
NO_BUILD =	Yes

PREFIX =	${VARBASE}/www

do-configure:
	@sed -i 's,^#!/usr/bin/env php.*,#!${MODPHP_BIN},' \
	    ${WRKSRC}/bin/icingacli

do-install:
	${INSTALL_DATA_DIR} ${PREFIX}/icinga-web2 \
	    ${PREFIX}/conf/modules.sample
	cd ${WRKSRC}; pax -rw ./ ${PREFIX}/icinga-web2/
	${SUBST_CMD} ${PREFIX}/icinga-web2/packages/files/apache/*conf
	find ${PREFIX}/icinga-web2 \( -name '*.orig' \
	    -or -name '*.beforesubst' \) -delete
	ln -s ${TRUEPREFIX}/icinga-web2/bin/icingacli \
	    ${WRKINST}/usr/local/bin/

.include <bsd.port.mk>
