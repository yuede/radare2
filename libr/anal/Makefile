include ../config.mk

EXTRA_TARGETS+=do
EXTRA_CLEAN=doclean

NAME=r_anal
DEPS=r_util r_db r_reg r_syscall
CFLAGS+=-DCORELIB -Iarch -I$(TOP)/shlr

LDFLAGS+=${BN_LIBS}

CURDIR=p/

include p/capstone.mk
LDFLAGS+=$(CS_LDFLAGS)
LDFLAGS+=$(SHLR)/java/libr_java.a

.PHONY: all plugins libs ${EXTRA_CLEAN}

all: plugins

plugins: ${LIBSO} ${LIBAR}
	@${MAKE} -C p all

include ${STATIC_ANAL_PLUGINS}

STATIC_OBJS=$(addprefix $(LTOP)/anal/p/,$(STATIC_OBJ))
OBJLIBS=meta.o reflines.o ref.o op.o fcn.o bb.o var.o
OBJLIBS+=cond.o value.o cc.o diff.o types.o fcnstore.o
OBJLIBS+=hint.o anal.o data.o xrefs.o esil.o sign.o
OBJLIBS+=anal_ex.o switch.o state.o cycles.o
OBJLIBS+=esil_stats.o esil_trace.o flirt.o labels.o
OBJLIBS+=esil2reil.o pin.o

OBJS=${STATIC_OBJS} ${OBJLIBS}

test tests: tests-esil

tests-esil:
	cd ../../radare2-regressions ; \
		sh run_tests.sh t.esil

.PHONY: do doclean

do:
	${MAKE} -C d

doclean:
	${MAKE} -C d clean

include $(LTOP)/rules.mk
