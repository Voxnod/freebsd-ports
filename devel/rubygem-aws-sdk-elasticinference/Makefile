PORTNAME=	aws-sdk-elasticinference
PORTVERSION=	1.53.0
CATEGORIES=	devel rubygems
MASTER_SITES=	RG

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	Official AWS Ruby gem for Amazon Elastic Inference (Amazon Elastic Inference)
WWW=		https://github.com/aws/aws-sdk-ruby/tree/version-3/gems/aws-sdk-elasticinference

LICENSE=	APACHE20
LICENSE_FILE=	${WRKSRC}/LICENSE.txt

DEPRECATED=	Deprecated by upstream
EXPIRATION_DATE=2025-03-31

RUN_DEPENDS=	rubygem-aws-sdk-core>=3.216.0<4:devel/rubygem-aws-sdk-core \
		rubygem-aws-sigv4>=1.5<2:devel/rubygem-aws-sigv4

USES=		gem

NO_ARCH=	yes

.include <bsd.port.mk>
