PORTNAME=	netgen
DISTVERSION=	1.5.290
CATEGORIES=	cad
PKGNAMESUFFIX=	-lvs

MAINTAINER=	yuri@FreeBSD.org
COMMENT=	Tool for comparing netlists (a process known as LVS)
WWW=		http://opencircuitdesign.com/netgen/

LICENSE=	GPLv1
LICENSE_FILE=	${WRKSRC}/Copying

RUN_DEPENDS=	bash:shells/bash

USES=		gmake python shebangfix tar:tgz tcl tk xorg
USE_XORG=	x11

USE_GITHUB=	yes
GH_ACCOUNT=	RTimothyEdwards

SHEBANG_FILES=	tcltk/netgen.sh.in

GNU_CONFIGURE=	yes
CONFIGURE_ENV=	HAVE_PYTHON3=yes
CONFIGURE_ARGS=	--with-interpreter=tcl --with-tcl=${LOCALBASE}/lib/tcl8.6 --with-tk=${LOCALBASE}/lib/tk8.6 --with-x

CONFLICTS_INSTALL=	netgen # bin/netgen

post-patch:
	@${REINPLACE_CMD} -e 's|^#!/bin/env python3$$|#!${PYTHON_CMD}|' \
		${WRKSRC}/python/*.py \
		${WRKSRC}/python/*.py.in

post-install:
	@${STRIP_CMD} ${STAGEDIR}${PREFIX}/lib/netgen/tcl/netgenexec ${STAGEDIR}${PREFIX}/lib/netgen/tcl/tclnetgen.so

.include <bsd.port.mk>
