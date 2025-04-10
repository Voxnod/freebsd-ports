PORTNAME=	neko
DISTVERSIONPREFIX=	v
DISTVERSION=	2-2-0
PORTREVISION=	13
CATEGORIES=	lang

MAINTAINER=	penzin.dev@gmail.com
COMMENT=	Neko programming languages and virtual machine
WWW=		https://nekovm.org/

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

DEPRECATED=	Depends on expired security/mbedtls2
EXPIRATION_DATE=2025-03-31

BUILD_DEPENDS=	git:devel/git
LIB_DEPENDS=	libgc-threaded.so:devel/boehm-gc-threaded \
		libapr-1.so:devel/apr1 libaprutil-1.so:devel/apr1 \
		libpcre.so:devel/pcre libpcreposix.so:devel/pcre \
		libmbedtls.so:security/mbedtls2 libmbedcrypto.so:security/mbedtls2 libmbedx509.so:security/mbedtls2 \
		libfontconfig.so:x11-fonts/fontconfig libfreetype.so:print/freetype2

USES=		cmake mysql pkgconfig sqlite:3
USE_GITHUB=	yes
GH_ACCOUNT=	HaxeFoundation
USE_LDCONFIG=	${PREFIX}/lib ${PREFIX}/lib/neko

MAKE_JOBS_UNSAFE=	yes

OPTIONS_DEFINE=	APACHE UI
OPTIONS_DEFAULT=	APACHE
OPTIONS_SUB=	yes
APACHE_DESC=	Build Apache modules
UI_DESC=	UI (GTK)

UI_USES=	gnome
UI_USE=		gnome=atk,cairo,gdkpixbuf,glib20,gtk20,pango
UI_CMAKE_BOOL=	WITH_UI

APACHE_USES=	apache
APACHE_CMAKE_BOOL=	WITH_APACHE

.include <bsd.port.mk>
