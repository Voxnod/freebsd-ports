PORTNAME=	gtfslib
PORTVERSION=	1.0.0
CATEGORIES=	devel python databases geography
MASTER_SITES=	PYPI
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	lbartoletti@FreeBSD.org
COMMENT=	Library for reading GTFS-based transit data in Python
WWW=		https://pypi.org/project/gtfslib/

LICENSE=	GPLv3+

DEPRECATED=	Depends on expired databases/py-sqlalchemy11
EXPIRATION_DATE=2024-06-04

RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}sqlalchemy11>=0.6.1:databases/py-sqlalchemy11@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}six>=1.9.0:devel/py-six@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}docopt>=0.6:devel/py-docopt@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}requests>=2.18:www/py-requests@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}pyqtree>=0.24:devel/py-pyqtree@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}pyshp>=1.2.12:devel/py-pyshp@${PY_FLAVOR}

NO_ARCH=	yes

USES=		python
USE_PYTHON=	autoplist distutils

.include <bsd.port.mk>
