PORTNAME=	stable-diffusion-environment
PORTVERSION=	1.0.0
CATEGORIES=	science linux
MASTER_SITES=	https://repo.anaconda.com/miniconda/
PKGNAMEPREFIX=	linux-
DISTNAME=	Miniconda3-${CONDA_VERSION}-Linux-x86_64.sh
EXTRACT_SUFX=
EXTRACT_ONLY=

MAINTAINER=	voxnod@gmail.com
COMMENT=	Linux python environment for Stable Diffusion demo

ONLY_FOR_ARCHS=	amd64

FETCH_DEPENDS=	linux_base-rl9>=9.2:emulators/linux_base-rl9
BUILD_DEPENDS=	linux-rl9-devtools>=0:devel/linux-rl9-devtools
RUN_DEPENDS=	linux-rl9-python${PYTHON_SUFFIX}>=0:lang/linux-rl9-python3

USES=		linux:rl9
USE_LINUX_PREFIX=	yes

DIST_SUBDIR=	${PORTNAME}

PLIST_SUB+=     PYTHON_SUFFIX=${PYTHON_SUFFIX} \
		PYTHON_VER=${PYTHON_VER}

CONDA_VERSION=	py39_25.1.1-2
PYTHON_SUFFIX=	39
PYTHON_VER=	3.9

post-fetch:
	@if [ ! -d "${DISTDIR}/${DIST_SUBDIR}/miniconda3/envs/pytorch" ]; then \
		${ECHO_MSG} "Miniconda environment 'pytorch' not found. Setting up..."; \
		${SETENV} HOME=${DISTDIR}/${DIST_SUBDIR} ${SH} ${DISTDIR}/${DIST_SUBDIR}/${DISTNAME} -b -s; \
		${DISTDIR}/${DIST_SUBDIR}/miniconda3/bin/conda create --name pytorch python=${PYTHON_VER} -y; \
		${LINUXBASE}/bin/bash -c "source ${DISTDIR}/${DIST_SUBDIR}/miniconda3/etc/profile.d/conda.sh && \
			conda activate pytorch && \
			pip install -r ${FILESDIR}/requirements.txt"; \
	fi

do-build:
	/compat/linux/bin/cc --sysroot=/compat/linux -m64 -std=c99 -Wall -ldl -fPIC -shared -o ${WRKDIR}/dummy-uvm.so ${FILESDIR}/uvm_ioctl_override.c

do-install:
	${MKDIR} ${STAGEDIR}${PREFIX}/usr/bin
	${FIND} ${DISTDIR}/${DIST_SUBDIR}/miniconda3/envs/pytorch/bin -type f -exec ${CP} {} ${STAGEDIR}${PREFIX}/usr/bin \;
	${MKDIR} ${STAGEDIR}${PREFIX}/usr/lib/python${PYTHON_VER}
	${CP} -r ${DISTDIR}/${DIST_SUBDIR}/miniconda3/envs/pytorch/lib/python${PYTHON_VER}/site-packages ${STAGEDIR}${PREFIX}/usr/lib/python${PYTHON_VER}
	for item in `cat ${FILESDIR}/redundant-items.txt`; do \
		${RM} -r ${STAGEDIR}${PREFIX}/usr/$$item; \
	done
	${FIND} ${STAGEDIR}${PREFIX}/usr/bin -type f -exec ${REINPLACE_CMD} -i '' 's|${DISTDIR}/${DIST_SUBDIR}/miniconda3/envs/pytorch/bin/python|/bin/python3|' {} +
	${MKDIR} ${STAGEDIR}${DATADIR}
	${INSTALL_LIB} ${WRKDIR}/dummy-uvm.so ${STAGEDIR}${DATADIR}

.include <bsd.port.mk>
