PORTNAME=	m17n-im-config
PORTVERSION=	0.9.0
PORTREVISION=	10
CATEGORIES=	textproc
MASTER_SITES=	http://www.m17n.org/common/im-config/ \
		http://anthesphoria.net/FreeBSD/ports/distfiles/

MAINTAINER=	nikola.lecic@anthesphoria.net
COMMENT=	GUI for per-user configuration of m17n-lib input methods
WWW=		https://www.m17n.org

DEPRECATED=	Upstream disapeared and distfile is no more available
EXPIRATION_DATE=2025-03-31

LIB_DEPENDS=	libm17n.so:devel/m17n-lib

MAKE_JOBS_UNSAFE=	yes

USE_GNOME=	gtk20 intltool intlhack glib20
USES=		gettext gnome libtool pathfix pkgconfig
USE_LDCONFIG=	yes
GNU_CONFIGURE=	yes
INSTALL_TARGET=	install-strip

DESKTOP_ENTRIES="M17N-IM Configuration" \
		"${COMMENT}" \
		"" \
		"m17n-im-config" \
		"Settings;" \
		true

OPTIONS_DEFINE=	NLS

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MNLS}
USES+=		gettext
CONFIGURE_ARGS+=	--enable-nls
PLIST_SUB+=	NLS=""
.else
CONFIGURE_ARGS+=	--disable-nls
PLIST_SUB+=	NLS="@comment "
.endif

.include <bsd.port.mk>
