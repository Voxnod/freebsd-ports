PORTNAME=	sfml
PORTVERSION=	2.5.1
PORTREVISION=	4
CATEGORIES=	devel
PKGNAMESUFFIX=	251

MAINTAINER=	amdmi3@FreeBSD.org
COMMENT=	Simple and Fast Multimedia Library
WWW=		https://www.sfml-dev.org/

LICENSE=	ZLIB
LICENSE_FILE=	${WRKSRC}/license.md

USE_GITHUB=	yes
GH_ACCOUNT=	SFML
GH_PROJECT=	SFML

USES=		cmake compiler:c++11-lang
USE_CXXSTD=	c++14
CMAKE_ARGS=	-DSFML_INSTALL_PKGCONFIG_FILES=ON \
		-DSFML_USE_SYSTEM_DEPS=ON
USE_LDCONFIG=	yes

CONFLICTS=	sfml

DATADIR=	${PREFIX}/share/SFML
PORTDATA=	*
PORTDOCS=	*
PORTEXAMPLES=	*

OPTIONS_DEFINE=	DOCS EXAMPLES DOXYGEN
OPTIONS_GROUP=	MODULES
OPTIONS_GROUP_MODULES=	WINDOW GRAPHICS AUDIO NETWORK
OPTIONS_DEFAULT=${OPTIONS_GROUP_MODULES}
OPTIONS_SUB=	yes

MODULES_DESC=	SFML modules

WINDOW_DESC=		SFML Window module
WINDOW_CMAKE_BOOL=	SFML_BUILD_WINDOW
WINDOW_USES=		gl xorg
WINDOW_USE=		XORG=x11,xrandr GL=gl

GRAPHICS_DESC=		SFML Graphics module
GRAPHICS_CMAKE_BOOL=	SFML_BUILD_GRAPHICS
GRAPHICS_LIB_DEPENDS=	libfreetype.so:print/freetype2
GRAPHICS_IMPLIES=	WINDOW

AUDIO_DESC=		SFML Audio module
AUDIO_CMAKE_BOOL=	SFML_BUILD_AUDIO
AUDIO_USES=		openal:al
AUDIO_LIB_DEPENDS=	libFLAC.so:audio/flac \
			libogg.so:audio/libogg \
			libvorbis.so:audio/libvorbis

NETWORK_DESC=		SFML Network module
NETWORK_CMAKE_BOOL=	SFML_BUILD_NETWORK

DOXYGEN_CMAKE_BOOL=	SFML_BUILD_DOC
DOXYGEN_BUILD_DEPENDS=	doxygen:devel/doxygen
DOXYGEN_IMPLIES=	DOCS

EXAMPLES_CMAKE_BOOL=	SFML_BUILD_EXAMPLES

post-install:
	@${RM} ${STAGEDIR}${PREFIX}/*.pc

post-install-DOCS-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/changelog.md ${WRKSRC}/readme.md \
		${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
