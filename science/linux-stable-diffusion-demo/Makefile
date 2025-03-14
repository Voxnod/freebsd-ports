PORTNAME=	stable-diffusion-demo
PORTVERSION=	1.0.0
CATEGORIES=	science linux
PKGNAMEPREFIX=	linux-
DISTFILES=

MAINTAINER=	voxnod@gmail.com
COMMENT=	Stable Diffusion demonstation script

RUN_DEPENDS=	linux-nvidia-libs>=0:x11/linux-nvidia-libs \
		linux-stable-diffusion-environment>=0:science/linux-stable-diffusion-environment \
		nvidia-driver>=0:x11/nvidia-driver

NO_BUILD=	yes
SUB_FILES=	${PORTNAME}

do-install:
	${MKDIR} ${STAGEDIR}${DATADIR}
	${INSTALL_SCRIPT} ${FILESDIR}/stable-diffusion-sample.py ${STAGEDIR}${DATADIR}
	${INSTALL_SCRIPT} ${WRKDIR}/${PORTNAME} ${STAGEDIR}${PREFIX}/bin/${PORTNAME}

.include <bsd.port.mk>
