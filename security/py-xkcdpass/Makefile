PORTNAME=	xkcdpass
DISTVERSIONPREFIX=	${PORTNAME}-
DISTVERSION=	1.17.4
PORTREVISION=	3
CATEGORIES=	security sysutils python
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	jacob@jwfh.ca
COMMENT=	Password generator as in XKCD 936
WWW=		https://github.com/jwfh/xkcdpass

LICENSE=	BSD3CLAUSE
LICENSE_FILE=	${WRKSRC}/LICENSE.BSD

TEST_DEPENDS=	${PYTHON_PKGNAMEPREFIX}mock>=0:devel/py-mock@${PY_FLAVOR}

USES=		python
USE_GITHUB=	yes
GH_ACCOUNT=	jwfh
USE_PYTHON=	autoplist concurrent distutils

NO_ARCH=	yes

PLIST_FILES=	${_MAN_FILES:S|^|share/man/man1/|:S|$|.gz|}

OPTIONS_DEFINE=	DOCS

DOCS_PLIST_FILES=	${_README_FILES:S|^|${DOCSDIR_REL}/|}

_MAN_FILES=	${PORTNAME}.1
_README_FILES=	README.rst

post-install:
	${INSTALL_MAN} ${_MAN_FILES:S|^|${WRKSRC}/|} ${STAGEDIR}${PREFIX}/share/man/man1

post-install-DOCS-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${_README_FILES:S|^|${WRKSRC}/|} ${STAGEDIR}${DOCSDIR}

do-test:
	@(cd ${TEST_WRKSRC} && \
		${SETENV} ${TEST_ENV} ${PYTHON_CMD} ${PYDISTUTILS_SETUP} test)

.include <bsd.port.mk>
