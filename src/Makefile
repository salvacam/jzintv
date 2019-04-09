CHAINPREFIX=/opt/mipsel-linux-uclibc
CROSS_COMPILE=$(CHAINPREFIX)/usr/bin/mipsel-linux-

BUILDTIME=$(shell date +'\"%Y-%m-%d %H:%M\"')

CC = $(CROSS_COMPILE)gcc
CXX = $(CROSS_COMPILE)g++
STRIP = $(CROSS_COMPILE)strip

SYSROOT     := $(CHAINPREFIX)/usr/mipsel-buildroot-linux-uclibc/sysroot
SDL_CFLAGS  := $(shell $(SYSROOT)/usr/bin/sdl-config --cflags)
SDL_LIBS    := $(shell $(SYSROOT)/usr/bin/sdl-config --libs)


##############################################################################
## Source-level Makefile for jzintv
##
## The whole make process is driven from the top-level Makefile.  In contrast
## to the (poor) advice given in the Make documentation, I do _not_ call make
## recursively to build the source of this project.
##############################################################################

##############################################################################
## Project directory structure
##############################################################################
B=../bin
L=../lib
R=../rom

##############################################################################
## Project-wide build flags
##############################################################################
P  = export PATH;

# Set "RM" to be the remove/delete command
RM = rm -f 


# WARN    = -Wall -W -Wshadow -Wpointer-arith \
#	       -Wbad-function-cast -Wcast-qual 
# WARNXX  = -Wall -W -Wshadow -Wpointer-arith -Wcast-qual 


#DEF_FLAGS = -DDIRECT_INTV2PC
#DEF_FLAGS = -DNEED_INOUT
DEF_FLAGS = -DGP2X -DGCWZERO 
#OPT_FLAGS  = -O2 #for release
#OPT_FLAGS = -ggdb 
# OPT_FLAGS = -O0 -g
#OPT_FLAGS = -O2 -ggdb
OPT_FLAGS = -O6 -fomit-frame-pointer -ggdb
#OPT_FLAGS = -pg -ggdb -DLOCAL=
#OPT_FLAGS = -tpp6 -axMiKW -ip -vec_report3 -opt_report -ansi_alias -restrict -DHAVE_RESTRICT -align -O3 -Ob1 # -ipo # intel icc flags

CFLAGS   = $(OPT_FLAGS) $(WARN)   -I. $(DEF_FLAGS) $(EXTRA)
CXXFLAGS = $(OPT_FLAGS) $(WARNXX) -I. -I.. $(DEF_FLAGS) $(EXTRA)
LFLAGS   = \
-lpthread \
-lSDL -lSDL_image -lSDL_ttf -lSDL_gfx \
-lpng -lz -lc -lm -ldl

OBJS=jzintv.o
PROG=$(B)/jzintv.dge
TOCLEAN=$(B)/jzintv.dge core

PROGS=$(PROG)

CFLAGS += $(SDL_CFLAGS)
LFLAGS += $(SDL_LIBS)

##############################################################################
## Generic build-rules
##############################################################################

all: $(OBJS) $(PROG)

$(PROG): $(OBJS)
	$(CC) -o $(PROG) $(OBJS) $(CFLAGS) $(LFLAGS)

clean:
	$(RM) $(OBJS) 
	$(RM) $(TOCLEAN)

%.o: %.c
	$(CC) -o $@ $(CFLAGS) -c $<

OBJS += plat/plat_gp2x.o
OBJS += pads/pads_cgc_linux.o

##############################################################################
## Makefile.common includes all the subMakefiles and such
##############################################################################
include Makefile.common
build: jzIntv
