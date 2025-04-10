PORTNAME=	terminator
DISTVERSION=	2.1.3
PORTREVISION=	3
CATEGORIES=	x11 python
MASTER_SITES=	https://github.com/gnome-${PORTNAME}/${PORTNAME}/releases/download/v${DISTVERSION}/

MAINTAINER=	ume@FreeBSD.org
COMMENT=	Multiple GNOME terminals in one window
WWW=		https://github.com/gnome-terminator/terminator

LICENSE=	GPLv2
LICENSE_FILE=	${WRKSRC}/COPYING

DEPRECATED=	Depends on expired devel/py-pytest-runner
EXPIRATION_DATE=2025-03-31

BUILD_DEPENDS=	${PYTHON_PKGNAMEPREFIX}pytest-runner>0:devel/py-pytest-runner@${PY_FLAVOR}
RUN_DEPENDS=	${LOCALBASE}/lib/libkeybinder-3.0.so:x11/keybinder-gtk3 \
		${LOCALBASE}/lib/libnotify.so:devel/libnotify \
		${PYTHON_PKGNAMEPREFIX}configobj>0:devel/py-configobj@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}psutil>0:sysutils/py-psutil@${PY_FLAVOR} \
		gsettings-desktop-schemas>=0:devel/gsettings-desktop-schemas

USES=		gnome python shebangfix gettext
USE_GNOME=	intltool pygobject3 vte3
USE_PYTHON=	autoplist distutils noflavors

PYDISTUTILS_PKGNAME=	Terminator

NO_ARCH=	yes

.include <bsd.port.mk>
