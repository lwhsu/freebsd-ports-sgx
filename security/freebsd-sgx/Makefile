# $FreeBSD$

PORTNAME=	freebsd-sgx
PORTVERSION=	1.9
CATEGORIES=	security
MASTER_SITES=	https://download.01.org/intel-sgx/linux-${PORTVERSION}/:optimized_libs
DISTFILES=	optimized_libs-${OPTIMIZED_LIB_VRSION}.tar:optimized_libs
DIST_SUBDIR=	${PORTNAME}

MAINTAINER=	lwhsu@FreeBSD.org
COMMENT=	FreeBSD support for Intel SGX SDK

LICENSE=	BSD3CLAUSE

BUILD_DEPENDS=	bash:shells/bash \
		ocamlbuild:lang/ocaml \
		protoc:devel/protobuf \
		autoreconf:devel/autoconf \
		automake:devel/automake

OPTIMIZED_LIB_VRSION=	1.9.100.39124

USES=	gmake libtool:build

USE_GITHUB=	yes
GH_ACCOUNT=	bukinr
GH_TAGNAME=	35a1069

USE_LDCONFIG=	yes

PLIST_FILES=\
	lib/libsgx_uae_service.so \
	lib/libsgx_urts.so \
	sbin/aesm_service

.include <bsd.port.pre.mk>

.if ${OSREL:R} < 12
IGNORE=	Intel SGX support is not available in FreeBSD-${OSREL:R}
.endif

post-extract:
	${MV} ${WRKDIR}/external/* ${WRKSRC}/external/

do-install:
	${INSTALL_PROGRAM} build/linux/aesm_service ${STAGEDIR}${PREFIX}/sbin
	${INSTALL_LIB} build/linux/libsgx_uae_service.so ${STAGEDIR}${PREFIX}/lib/
	${INSTALL_LIB} build/linux/libsgx_urts.so ${STAGEDIR}${PREFIX}/lib/

.include <bsd.port.post.mk>
