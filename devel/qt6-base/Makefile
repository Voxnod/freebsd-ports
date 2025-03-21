PORTNAME=	base
DISTVERSION=	${QT6_VERSION}
PORTREVISION=	4
CATEGORIES=	devel
PKGNAMEPREFIX=	qt6-

PATCH_SITES=	https://invent.kde.org/qt/qt/qtbase/-/commit/
PATCHFILES+=	12d4bf1ab52748cb84894f50d437064b439e0b7d.patch:-p1
PATCHFILES+=	2ef615228bba9a8eb282437bfb7472f925610e89.patch:-p1
PATCHFILES+=	a43c7e58046604796aa69974ea1c5d3e2648c755.patch:-p1

MAINTAINER=	kde@FreeBSD.org
COMMENT=	Qt base (core, gui, widgets, network,...)

BUILD_DEPENDS=	xml:textproc/xmlstarlet \
		${LOCALBASE}/include/vulkan/vulkan.h:graphics/vulkan-headers \
		${LOCALBASE}/include/linux/input.h:devel/evdev-proto
LIB_DEPENDS=	libatk-1.0.so:accessibility/at-spi2-core \
		libatk-bridge-2.0.so:accessibility/at-spi2-core \
		libatspi.so:accessibility/at-spi2-core \
		libb2.so:devel/libb2 \
		libbrotlidec.so:archivers/brotli \
		libdbus-1.so:devel/dbus \
		libdouble-conversion.so:devel/double-conversion \
		libdrm.so:graphics/libdrm \
		libevdev.so:devel/libevdev \
		libfontconfig.so:x11-fonts/fontconfig \
		libfreetype.so:print/freetype2 \
		libgraphite2.so:graphics/graphite2 \
		libharfbuzz.so:print/harfbuzz \
		libicui18n.so:devel/icu \
		libinput.so:x11/libinput \
		libintl.so:devel/gettext-runtime \
		libjpeg.so:graphics/jpeg-turbo \
		libmtdev.so:devel/libmtdev \
		libpcre2-16.so:devel/pcre2 \
		libpng16.so:graphics/png \
		libudev.so:devel/libudev-devd \
		libvulkan.so:graphics/vulkan-loader \
		libwayland-client.so:graphics/wayland \
		libxkbcommon.so:x11/libxkbcommon \
		libzstd.so:archivers/zstd

USES=		cmake compiler:c++17-lang gl gnome jpeg perl5 pkgconfig python \
		qt-dist:6 shebangfix ssl
USE_GL=		egl opengl
USE_GNOME=	cairo gdkpixbuf2 glib20 gtk30 pango
USE_LDCONFIG=	${PREFIX}/${QT_LIBDIR_REL}
USE_LOCALE=	C.UTF-8

SHEBANG_FILES=	${WRKSRC}/libexec/qt-android-runner.py \
		${WRKSRC}/mkspecs/features/uikit/device_destinations.sh \
		${WRKSRC}/mkspecs/features/uikit/devices.py \
		${WRKSRC}/mkspecs/features/data/mac/objc_namespace.sh \
		${WRKSRC}/util/testrunner/qt-testrunner.py \
		${WRKSRC}/util/testrunner/sanitizer-testrunner.py

CMAKE_ARGS=	-DOPENSSL_ROOT_DIR="${OPENSSLBASE}"
CMAKE_ON=	CMAKE_DISABLE_FIND_PACKAGE_LTTngUST \
		QT_AVOID_CMAKE_ARCHIVING_API \
		QT_FIND_ALL_PACKAGES_ALWAYS \
		QT_FEATURE_openssl_linked
CMAKE_OFF=	QT_FEATURE_eglfs \
		QT_FEATURE_gssapi
# sql drivers are handled in the databases/qt6-base_sqldriver port
CMAKE_OFF+=	FEATURE_sql_mysql \
		FEATURE_sql_odbc \
		FEATURE_sql_psql \
		FEATURE_sql_sqlite

# zstd from base fails to compress files during the build (error 11: unsupported argument)
BINARY_ALIAS=	zstd=${LOCALBASE}/bin/zstd

OPTIONS_DEFINE=		CUPS X11
OPTIONS_DEFAULT=	CUPS X11
OPTIONS_SUB=		yes

CUPS_LIB_DEPENDS=	libcups.so:print/cups
CUPS_CMAKE_BOOL=	FEATURE_cups

X11_LIB_DEPENDS=	libxcb-cursor.so:x11/xcb-util-cursor \
			libxcb-icccm.so:x11/xcb-util-wm \
			libxcb-image.so:x11/xcb-util-image \
			libxcb-keysyms.so:x11/xcb-util-keysyms \
			libxcb-render-util.so:x11/xcb-util-renderutil
X11_USES=		xorg
X11_USE=		XORG=ice,pixman,sm,x11,xau,xcb,xcomposite,xcursor,xdamage,xdmcp,xext,xfixes,xi,xinerama,xrandr,xrender
X11_CMAKE_BOOL=		FEATURE_xcb \
			FEATURE_xlib

.include <bsd.port.pre.mk>

# LibreSSL does not currently support BIO_ADDR in DTLSv1_listen()
.if ${SSL_DEFAULT:Mlibressl*}
CMAKE_OFF+=	QT_FEATURE_dtls
PLIST_SUB+=	DTLS="@comment "
.else
PLIST_SUB+=	DTLS=""
.endif

.if ${ARCH} == "armv6" || ${ARCH} == "armv7"
BUILD_DEPENDS+=	as:devel/binutils
CMAKE_ARGS+=	-DCMAKE_ASM_FLAGS=-no-integrated-as
.endif

post-patch:
	@${REINPLACE_CMD} -e 's|%%OPENSSLLIB%%|${OPENSSLLIB}|g' \
		${WRKSRC}/src/plugins/tls/openssl/qsslsocket_openssl_symbols.cpp

# TODO: do this cleaner -- somewhere cmake/qmake still creates empty directories
# for the cmake files in INSTALL_PREFIX/lib/cmake
post-install:
	${RM} -vr ${STAGEDIR}${PREFIX}/${QT_LIBDIR_REL}/cmake
	# Install symlinks for user-facing tools
	${REINPLACE_CMD} -e "s#^#${STAGEDIR}#" -e "s# # ${STAGEDIR}#" \
		${WRKDIR}/.build/user_facing_tool_links.txt
	while read t; do \
		${RLN} $$t; \
	done <${WRKDIR}/.build/user_facing_tool_links.txt

.include <bsd.port.post.mk>
