PORTNAME=	vanguards
DISTVERSION=	0.3.1
PORTREVISION=	1
CATEGORIES=	security python
MASTER_SITES=	PYPI
PKGNAMESUFFIX=	-tor

MAINTAINER=	yuri@FreeBSD.org
COMMENT=	Tor add-on to protect against guard discovery and related attacks
WWW=		https://github.com/mikeperry-tor/vanguards

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}stem>0:security/py-stem@${PY_FLAVOR}
TEST_DEPENDS=	${PYTHON_PKGNAMEPREFIX}pytest>0:devel/py-pytest@${PY_FLAVOR}

USES=		python
USE_PYTHON=	distutils autoplist noflavors
NO_ARCH=	yes

do-test: # 3 testcases are known to fail: https://github.com/mikeperry-tor/vanguards/issues/27
	@cd ${WRKSRC} && ${SETENV} ${MAKE_ENV} PYTHONPATH=${WRKSRC}/src ${PYTHON_CMD} -m pytest -rs tests

.include <bsd.port.mk>
