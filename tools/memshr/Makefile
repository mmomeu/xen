XEN_ROOT = $(CURDIR)/../..
include $(XEN_ROOT)/tools/Rules.mk

LIBMEMSHR-BUILD := libmemshr.a

CFLAGS          += -Werror
CFLAGS          += -Wno-unused
CFLAGS          += $(CFLAGS_xeninclude)
CFLAGS          += $(CFLAGS_libxenctrl)
CFLAGS          += -D_GNU_SOURCE
CFLAGS          += -fPIC

LIB-SRCS        := interface.c
LIB-SRCS        += shm.c
LIB-SRCS        += bidir-daemon.c
LIB-SRCS        += bidir-hash.c

LIB-OBJS        := interface.o
LIB-OBJS        += shm.o
LIB-OBJS        += bidir-daemon.o
LIB-OBJS        += bidir-hash-fgprtshr.o
LIB-OBJS        += bidir-hash-blockshr.o

all: build

build: $(LIBMEMSHR-BUILD)

bidir-hash-fgprtshr.o: bidir-hash.c
	$(CC) $(CFLAGS) -DFINGERPRINT_MAP -c -o $*.o bidir-hash.c 

bidir-hash-blockshr.o: bidir-hash.c
	$(CC) $(CFLAGS) -DBLOCK_MAP -c -o $*.o bidir-hash.c 

libmemshr.a: $(LIB-OBJS)
	$(AR) rc $@ $^

install: all

uninstall:

clean:
	rm -rf *.a *.o *~ $(DEPS_RM)

.PHONY: distclean
distclean: clean

.PHONY: all build clean install distclean uninstall

-include $(DEPS_INCLUDE)
