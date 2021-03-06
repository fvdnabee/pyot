# Makefile for libcoap
#
# Copyright (C) 2010--2013 Olaf Bergmann <bergmann@tzi.org>
#
# This file is part of the CoAP library libcoap. Please see
# README for terms of use. 

# the library's version
VERSION:=4.0.1

# tools

SHELL = /bin/sh
MKDIR = mkdir
ETAGS = /bin/false

abs_builddir = /home/andrea/repos/rtn/common/library/generic/contikiSnm/coapyGw/appsTesting/libcoap-4.0.1
top_builddir = .
package = libcoap-4.0.1

# files and flags
SOURCES:= pdu.c net.c debug.c encode.c uri.c coap_list.c resource.c hashkey.c \
	 str.c option.c async.c subscribe.c block.c
OBJECTS:= $(patsubst %.c, %.o, $(SOURCES))
HEADERS:=coap.h config.h debug.h pdu.h net.h encode.h uri.h coap_list.h mem.h \
	str.h option.h bits.h uthash.h utlist.h resource.h hashkey.h async.h \
	subscribe.h block.h address.h prng.h coap_time.h
CFLAGS:=-Wall -Wextra -std=c99 -pedantic -g -O2
CPPFLAGS:=
DISTDIR=$(top_builddir)/$(package)
SUBDIRS:=examples doc 
FILES:=ChangeLog README LICENSE.BSD LICENSE.GPL Makefile.in configure configure.in config.h.in $(SOURCES) $(HEADERS)
LIB:=libcoap.a
LDFLAGS:=
ARFLAGS:=cru
examples:=examples
doc:=doc


.PHONY: all dirs clean distclean .gitignore doc TAGS

.SUFFIXES:
.SUFFIXES:      .c .o

all:	$(LIB) dirs

check:	
	echo DISTDIR: $(DISTDIR)
	echo top_builddir: $(top_builddir)
	$(MAKE) -C examples check

dirs:	$(SUBDIRS)
	for dir in $^; do \
		$(MAKE) -C $$dir ; \
	done

$(LIB):	$(OBJECTS)
	$(AR) $(ARFLAGS) $@ $^ 
	ranlib $@

clean:
	@rm -f $(PROGRAM) main.o $(LIB) $(OBJECTS)
	for dir in $(SUBDIRS); do \
		$(MAKE) -C $$dir clean ; \
	done

doc:	
	$(MAKE) -C doc

distclean:	clean
	@rm -rf $(DISTDIR)
	@rm -f *~ $(DISTDIR).tar.gz

dist:	$(FILES) $(SUBDIRS)
	test -d $(DISTDIR) || mkdir $(DISTDIR)
	cp $(FILES) $(DISTDIR)
	for dir in $(SUBDIRS); do \
		$(MAKE) -C $$dir dist; \
	done
	tar czf $(package).tar.gz $(DISTDIR)

TAGS:	
	$(ETAGS) -o $@.new $(SOURCES) 
	$(ETAGS) -a -o $@.new $(HEADERS) 
	mv $@.new $@

.gitignore:
	echo "core\n*~\n*.[oa]\n*.gz\n*.cap\n$(PROGRAM)\n$(DISTDIR)\n.gitignore" >$@
