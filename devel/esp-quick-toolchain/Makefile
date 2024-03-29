PORTNAME=	esp-quick-toolchain
DISTVERSION=	3.1.0
CATEGORIES=	devel
MASTER_SITES=	\
	GNU/gmp/:src_gmp \
	GNU/mpfr/:src_mpfr \
	GNU/mpc/:src_mpc \
	https://libisl.sourceforge.io/:src_isl \
	https://gcc.gnu.org/pub/gcc/infrastructure/:src_cloog \
	https://github.com/earlephilhower/esp-quick-toolchain/raw/master/blobs/:src_libelf

# XXX see .stage.prepgit in Makefile
DISTFILES=	\
	gmp-6.1.0.tar.bz2:src_gmp \
	mpfr-3.1.4.tar.bz2:src_mpfr \
	mpc-1.0.3.tar.gz:src_mpc \
	isl-0.18.tar.bz2:src_isl \
	cloog-0.18.1.tar.gz:src_cloog \
	libelf-0.8.13.tar.gz:src_libelf

MAINTAINER=	y@trombik.org
COMMENT=	GCC toolchain for esp8266/arduino

LICENSE=	GPLv2

ONLY_FOR_ARCHS=	amd64
ONLY_FOR_ARCHS_REASON=	not ported to other ARCH

LIB_DEPENDS=	\
	libmpfr.so:math/mpfr \
	libgmp.so:math/gmp
BUILD_DEPENDS=	bash:shells/bash \
	autoconf>=2.69:devel/autoconf \
	automake>=1.16.1:devel/automake

USES=	gmake makeinfo tar:bzip2 python:build shebangfix libtool iconv
# use FLAVORS so that different versions of tool-chain can be installed.
FLAVORS=	gcc103
FLAVOR?=	${FLAVORS:[1]}

# the upstream
# https://github.com/earlephilhower/esp-quick-toolchain
EQT_GHUSER=	earlephilhower
# patched for FreeBSD
# https://github.com/kmihaylov/esp-quick-toolchain
# https://github.com/earlephilhower/esp-quick-toolchain/issues/28
EQT_FREEBSD_GHUSER=	kmihaylov

USE_GCC=	9+
BINARY_ALIAS=	make=${GMAKE}
SHEBANG_FILES=	*.py
USE_GITHUB=	yes
MAKE_ARGS+=	GCC=${EQT_GCC_VERSION} GHUSER=${EQT_GHUSER} GHTOKEN=dummy
ALL_TARGET=	freebsd
GH_TUPLE=	\
	${EQT_GHUSER}:${PORTNAME}:${EQT_GITREF} \
	${EQT_GHUSER}:newlib-xtensa:${EQT_GITREF_NEWLIB}:src_newlib_xtensa/repo/newlib \
	${EQT_GHUSER}:lx106-hal:${EQT_GITREF_LX106_HAL}:src_lx106_hal/repo/lx106-hal \
	${EQT_GHUSER}:mkspiffs:${EQT_GITREF_MKSPIFFS}:src_mkspiffs/repo/mkspiffs \
	${EQT_GHUSER}:mklittlefs:${EQT_GITREF_MKLITTLEFS}:src_mklittlefs/repo/mklittlefs \
	${EQT_GHUSER}:esptool-ck:${EQT_GITREF_ESPTOOL_CK}:src_esptool_ck/repo/esptool \
	pellepl:spiffs:${EQT_GITREF_SPIFFS}:src_spiffs/repo/mkspiffs/spiffs \
	littlefs-project:littlefs:${EQT_GITREF_LITTLEFS}:src_littlefs/repo/mklittlefs/littlefs \
	esp8266:Arduino:${EQT_GITREF_ARDUINO}:src_arduino/arduino \
	d-a-v:esp82xx-nonos-linklayer:${EQT_GITREF_ARDUINO_ESP82XX_NONOS_LINKLAYER}:src_arduino_module_1/arduino/tools/sdk/lwip2/builder \
	earlephilhower:bearssl-esp8266:${EQT_GITREF_ARDUINO_BEARSSL_ESP8266}:src_arduino_module_2/arduino/tools/sdk/ssl/bearssl \
	plerup:espsoftwareserial:${EQT_GITREF_ARDUINO_ESPSOFTWARESERIAL}:src_arduino_module_3/arduino/libraries/SoftwareSerial \
	ARMmbed:littlefs:${EQT_GITREF_ARDUINO_LITTLEFS}:src_arduino_module_4/arduino/libraries/LittleFS/lib/littlefs \
	earlephilhower:ESP8266SdFat:${EQT_GITREF_ARDUINO_ESP8266SDFAT}:src_arduino_module_5/arduino/libraries/ESP8266SdFat \
	pyserial:pyserial:${EQT_GITREF_ARDUINO_PYSERIAL}:src_arduino_module_6/arduino/tools/pyserial \
	espressif:esptool:${EQT_GITREF_ARDUINO_ESPTOOL}:src_arduino_module_7/arduino/tools/esptool \
	arduino-libraries:Ethernet:${EQT_GITREF_ARDUINO_ETHERNET}:src_arduino_module_8/arduino/libraries/Ethernet \
	pfalcon:uzlib:${EQT_GITREF_ARDUINO_UZLIB}:src_arduino_module_9/arduino/tools/sdk/uzlib \
	lwip-tcpip:lwip:${EQT_GITREF_LWIP2}:src_lwip2/arduino/tools/sdk/lwip2/builder/lwip2-src

# XXX the Makefile of ${PORTNAME} uses branches instead of specific tags or
# commit refs.
EQT_GITREF=	${DISTVERSION}-gcc10.3
EQT_GITREF_NEWLIB=	ebc9675
EQT_GITREF_LX106_HAL=	e4bcc63c
EQT_GITREF_MKSPIFFS=	7fefeac
EQT_GITREF_MKLITTLEFS=	30b7fc1
EQT_GITREF_ESPTOOL_CK=	f80ae31
# XXX git submodules
EQT_GITREF_SPIFFS=		f5e26c4e
EQT_GITREF_LITTLEFS=	1863dc78

# XXX https://github.com/esp8266/Arduino/releases
EQT_GITREF_ARDUINO=	3.0.2
# XXX git submodules of esp8266/Arduino
EQT_GITREF_ARDUINO_ESP82XX_NONOS_LINKLAYER=	7421258
EQT_GITREF_ARDUINO_BEARSSL_ESP8266=	6105635
EQT_GITREF_ARDUINO_ESPSOFTWARESERIAL=	566809f
EQT_GITREF_ARDUINO_LITTLEFS=	1a59954
EQT_GITREF_ARDUINO_ESP8266SDFAT=	9472c86
EQT_GITREF_ARDUINO_PYSERIAL=	0e76347
EQT_GITREF_ARDUINO_ESPTOOL=	4fa0bd7
EQT_GITREF_ARDUINO_ETHERNET=	75a3c37
EQT_GITREF_ARDUINO_UZLIB=	27e4f4c
# XXX git submodule (actually, clone) of d-a-v/esp82xx-nonos-linklayer
# see esp82xx-nonos-linklayer/makefiles/Makefile.defs
EQT_GITREF_LWIP2=	STABLE-2_1_2_RELEASE

gcc103_PKGNAMESUFFIX=	-${FLAVOR}
gcc103_PLIST= ${.CURDIR}/pkg-plist.${FLAVOR}
DISTINFO_FILE=	${MASTERDIR}/distinfo.${FLAVOR}

# XXX timestamp of the build. see the release page at:
# https://github.com/earlephilhower/esp-quick-toolchain/releases
# the value is the last digits in file names. an example:
# aarch64-linux-gnu.esptool-f80ae31.210605.tar.gz
EQT_STAMP=	220621
EQT_STRIP_FILES=	\
	lib/gcc/xtensa-lx106-elf/${EQT_GCC_VERSION_FULL}/plugin/libcc1plugin.so.0 \
	lib/gcc/xtensa-lx106-elf/${EQT_GCC_VERSION_FULL}/plugin/libcp1plugin.so.0 \
	lib/libcc1.so.0 \
	libexec/gcc/xtensa-lx106-elf/${EQT_GCC_VERSION_FULL}/install-tools/fixincl \
	libexec/gcc/xtensa-lx106-elf/${EQT_GCC_VERSION_FULL}/liblto_plugin.so.0 \
	libexec/gcc/xtensa-lx106-elf/${EQT_GCC_VERSION_FULL}/lto-wrapper \
	libexec/gcc/xtensa-lx106-elf/${EQT_GCC_VERSION_FULL}/plugin/gengtype

.if ${FLAVOR} == gcc103
EQT_GCC_VERSION=	10.3
EQT_GCC_VERSION_FULL=	10.3.0
EQT_PIO_VERSION=	5.100300.${EQT_STAMP}
EQT_GITREF_GCC=	releases/gcc-10.3.0
EQT_GITREF_BINUTILS=	binutils-2_32
EQT_BINUTILS_DIR=	binutils-gdb-gnu
GH_TUPLE+=	gcc-mirror:gcc:${EQT_GITREF_GCC}:src_gcc_gnu/repo/gcc-gnu \
	bminor:binutils-gdb:${EQT_GITREF_BINUTILS}:src_binutils_gdb/repo/${EQT_BINUTILS_DIR}
.endif
EQT_DESTDIR=	${PREFIX}/${PORTNAME}-${FLAVOR}

post-extract:
	${MKDIR} ${WRKSRC}/repo
.for F in ${DISTFILES}
	# make target, ".stage.prepgit", expects files here
	(cd ${WRKSRC}/repo && ${LN} -s ${DISTDIR}/${F:C/:.*//} .)
.endfor
	# XXX applied in:
	# https://github.com/earlephilhower/mkspiffs/commit/24124efae6b82621bbf66ce6fb9740e08a07f51b
	${RM} ${WRKSRC}/patches/mkspiffs/0.2.0-makefile.patch

pre-configure:
	@${REINPLACE_CMD} \
		-e 's,%%CC%%,${CC},g' \
		-e 's,%%CXX%%,${CXX},g' \
		-e 's,%%ARCH%%,${ARCH},g' \
		-e 's,%%EQT_GITREF%%,${EQT_GITREF},g' \
		-e 's,%%EQT_GITREF_SPIFFS%%,${EQT_GITREF_SPIFFS},g' \
		-e 's,%%EQT_GITREF_MKLITTLEFS%%,${EQT_GITREF_MKLITTLEFS},g' \
		-e 's,%%EQT_GITREF_ESPTOOL_CK%%,${EQT_GITREF_ESPTOOL_CK},g' \
		-e 's,%%EQT_STAMP%%,${EQT_STAMP},g' \
		${WRKSRC}/Makefile
	@${REINPLACE_CMD} \
		-e 's,%%EQT_GITREF_ARDUINO_BEARSSL_ESP8266%%,${EQT_GITREF_ARDUINO_BEARSSL_ESP8266},g' \
		${WRKSRC}/arduino/tools/sdk/ssl/Makefile
	@${REINPLACE_CMD} \
		-e 's,%%EQT_GITREF_ARDUINO_ESP82XX_NONOS_LINKLAYER%%,${EQT_GITREF_ARDUINO_ESP82XX_NONOS_LINKLAYER},g' \
		-e 's,%%EQT_GITREF_LWIP2%%,${EQT_GITREF_LWIP2},g' \
		${WRKSRC}/arduino/tools/sdk/lwip2/builder/makefiles/make-lwip-hash

do-install:
	${INSTALL} -d ${STAGEDIR}${EQT_DESTDIR}
	# example: x86_64-portbld-freebsd14.0.xtensa-lx106-elf-a114ba5.210619.tar.gz
	${TAR} -x \
		-C ${STAGEDIR}${EQT_DESTDIR} \
		-f ${WRKSRC}/x86_64-portbld-freebsd${OSREL}.xtensa-lx106-elf-${EQT_GITREF}.${EQT_STAMP}.tar.gz
	${TAR} -x \
		-C ${STAGEDIR}${EQT_DESTDIR} \
		-f ${WRKSRC}/x86_64-portbld-freebsd${OSREL}.esptool-${EQT_GITREF_ESPTOOL_CK}.${EQT_STAMP}.tar.gz
	${TAR} -x \
		-C ${STAGEDIR}${EQT_DESTDIR} \
		-f ${WRKSRC}/x86_64-portbld-freebsd${OSREL}.mklittlefs-${EQT_GITREF_MKLITTLEFS}.${EQT_STAMP}.tar.gz
	${TAR} -x \
		-C ${STAGEDIR}${EQT_DESTDIR} \
		-f ${WRKSRC}/x86_64-portbld-freebsd${OSREL}.mkspiffs-${EQT_GITREF_SPIFFS}.${EQT_STAMP}.tar.gz
	(cd ${STAGEDIR}${EQT_DESTDIR}/xtensa-lx106-elf && ${STRIP_CMD} ${EQT_STRIP_FILES})

	# XXX create .piopm, which is (yet another) undocumented new metadata
	# file. pio 3.x expects "owner" metadata field, which is NOT in
	# package.json.  without .piopm, pio rejects packages because "owner" is
	# not "platformio" but None (i.e. unknown owner). see the logic in
	# "test_pkg_spec" at:
	# platformio/package/manager/base.py
	${CP} ${FILESDIR}/toolchain-xtensa.piopm ${WRKSRC}
	${CP} ${FILESDIR}/tool-esptool.piopm ${WRKSRC}
	${CP} ${FILESDIR}/tool-mkspiffs.piopm ${WRKSRC}
	${CP} ${FILESDIR}/tool-mklittlefs.piopm ${WRKSRC}
	${REINPLACE_CMD} \
		-e 's,%%EQT_PIO_VERSION%%,${EQT_PIO_VERSION},' \
		${WRKSRC}/toolchain-xtensa.piopm \
		${WRKSRC}/tool-esptool.piopm \
		${WRKSRC}/tool-mkspiffs.piopm \
		${WRKSRC}/tool-mklittlefs.piopm
	${INSTALL_DATA} ${WRKSRC}/toolchain-xtensa.piopm ${STAGEDIR}${EQT_DESTDIR}/xtensa-lx106-elf/.piopm
	${INSTALL_DATA} ${WRKSRC}/tool-esptool.piopm ${STAGEDIR}${EQT_DESTDIR}/esptool/.piopm
	${INSTALL_DATA} ${WRKSRC}/tool-mklittlefs.piopm ${STAGEDIR}${EQT_DESTDIR}/mklittlefs/.piopm
	${INSTALL_DATA} ${WRKSRC}/tool-mkspiffs.piopm ${STAGEDIR}${EQT_DESTDIR}/mkspiffs/.piopm

.include <bsd.port.mk>
