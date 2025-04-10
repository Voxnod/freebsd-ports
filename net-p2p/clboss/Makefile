PORTNAME=	clboss
DISTVERSIONPREFIX=	v
# To build from an arbitrary git commit comment DISTVERSION
DISTVERSION=	0.14.1
# and uncomment the following two lines (use for example -gf8d8348c where f8d8348c is a commit hash)
#DISTVERSION=	0
#DISTVERSIONSUFFIX=	-g0673c50e7
CATEGORIES=	net-p2p finance
.if defined(DISTVERSIONSUFFIX)
PKGNAMESUFFIX=	-devel
.endif

MAINTAINER=	vd@FreeBSD.org
COMMENT=	Core Lightning Node Manager
WWW=		https://github.com/ZmnSCPxj/clboss

LICENSE=	MIT

BUILD_DEPENDS=	autoconf-archive>=0:devel/autoconf-archive
LIB_DEPENDS=	libcurl.so:ftp/curl \
		libev.so:devel/libev \
		libunwind.so:devel/libunwind
RUN_DEPENDS=	lightningd:net-p2p/c-lightning

USES=		autoreconf \
		compiler:c11 \
		gmake \
		libtool \
		pkgconfig \
		sqlite:3

PATCH_STRIP=	-p1

CXXFLAGS+=	-Wno-deprecated-declarations
LDFLAGS+=	-lexecinfo

GNU_CONFIGURE=	yes

USE_GITHUB=	yes
GH_ACCOUNT=	ZmnSCPxj

SUB_FILES=	pkg-message
PLIST_FILES=	bin/clboss

post-patch:
	echo "#pragma once" > ${WRKSRC}/commit_hash.h
	echo "#define GIT_COMMIT_HASH \"d5955419e3bea3f0414affc4a4994043abc0a726\"" >> ${WRKSRC}/commit_hash.h
	echo "#define GIT_DESCRIBE \"v0.14.0-0-gd595541-dirty\"" >> ${WRKSRC}/commit_hash.h

.include <bsd.port.mk>
