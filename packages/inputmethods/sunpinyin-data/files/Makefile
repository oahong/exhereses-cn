#!/usr/bin/make -f
# -*- mode: makefile; indent-tabs-mode: t -*- vim:noet:ts=4
# Sample Makefile for lexicon generation and installation.

# Little endian platforms: alpha amd64 arm hurd-i386 i386 ia64 mipsel sh3 sh4
# Big endian platforms: hppa m68k mips powerpc ppc64 sparc s390
ifndef ENDIANNESS
	ENDIANNESS = le
endif

DICT_FILE = dict.utf8

SLM_TARGET = lm_sc
TSLM3_TEXT_FILE = ${SLM_TARGET}.t3g.arpa
TSLM3_ORIG_FILE = ${SLM_TARGET}.t3g.orig
TSLM3_DIST_FILE = ${SLM_TARGET}.t3g

PYTRIE_FILE = pydict_sc.bin
PYTRIE_LOG_FILE = pydict_sc.log

SYSTEM_DATA_DIR = ${DESTDIR}/usr/share/sunpinyin

all: slm3_dist
install: slm3_install

${TSLM3_ORIG_FILE}: ${DICT_FILE} ${TSLM3_TEXT_FILE}
	tslmpack ${TSLM3_TEXT_FILE} ${DICT_FILE} $@

${TSLM3_DIST_FILE}: ${TSLM3_ORIG_FILE}
	tslmendian -e ${ENDIANNESS} -i $^ -o $@

${PYTRIE3_FILE}: ${DICT_FILE} ${TSLM3_ORIG_FILE}
	genpyt -e ${ENDIANNESS} -i ${DICT_FILE} \
		-s ${TSLM3_ORIG_FILE} -l ${PYTRIE3_LOG_FILE} -o $@

slm3_dist: ${TSLM3_DIST_FILE} ${PYTRIE3_FILE}
slm3_install: ${TSLM3_DIST_FILE} ${PYTRIE3_FILE}
	install -d ${SYSTEM_DATA_DIR}
	install -Dm644 $^ ${SYSTEM_DATA_DIR}

