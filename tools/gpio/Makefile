# SPDX-License-Identifier: GPL-2.0
include ../scripts/Makefile.include

bindir ?= /usr/bin

<<<<<<< HEAD
ifeq ($(srctree),)
=======
# This will work when gpio is built in tools env. where srctree
# isn't set and when invoked from selftests build, where srctree
# is set to ".". building_out_of_srctree is undefined for in srctree
# builds
ifndef building_out_of_srctree
>>>>>>> abf4fbc657532dbe8f302d9ce2d78dbd2a009b82
srctree := $(patsubst %/,%,$(dir $(CURDIR)))
srctree := $(patsubst %/,%,$(dir $(srctree)))
endif

# Do not use make's built-in rules
# (this improves performance and avoids hard-to-debug behaviour);
MAKEFLAGS += -r

CFLAGS += -O2 -Wall -g -D_GNU_SOURCE -I$(OUTPUT)include

ALL_TARGETS := lsgpio gpio-hammer gpio-event-mon
ALL_PROGRAMS := $(patsubst %,$(OUTPUT)%,$(ALL_TARGETS))

all: $(ALL_PROGRAMS)

export srctree OUTPUT CC LD CFLAGS
include $(srctree)/tools/build/Makefile.include

#
# We need the following to be outside of kernel tree
#
$(OUTPUT)include/linux/gpio.h: ../../include/uapi/linux/gpio.h
	mkdir -p $(OUTPUT)include/linux 2>&1 || true
	ln -sf $(CURDIR)/../../include/uapi/linux/gpio.h $@

prepare: $(OUTPUT)include/linux/gpio.h

<<<<<<< HEAD
=======
GPIO_UTILS_IN := $(output)gpio-utils-in.o
$(GPIO_UTILS_IN): prepare FORCE
	$(Q)$(MAKE) $(build)=gpio-utils

>>>>>>> abf4fbc657532dbe8f302d9ce2d78dbd2a009b82
#
# lsgpio
#
LSGPIO_IN := $(OUTPUT)lsgpio-in.o
<<<<<<< HEAD
$(LSGPIO_IN): prepare FORCE
=======
$(LSGPIO_IN): prepare FORCE $(OUTPUT)gpio-utils-in.o
>>>>>>> abf4fbc657532dbe8f302d9ce2d78dbd2a009b82
	$(Q)$(MAKE) $(build)=lsgpio
$(OUTPUT)lsgpio: $(LSGPIO_IN)
	$(QUIET_LINK)$(CC) $(CFLAGS) $(LDFLAGS) $< -o $@

#
# gpio-hammer
#
GPIO_HAMMER_IN := $(OUTPUT)gpio-hammer-in.o
<<<<<<< HEAD
$(GPIO_HAMMER_IN): prepare FORCE
=======
$(GPIO_HAMMER_IN): prepare FORCE $(OUTPUT)gpio-utils-in.o
>>>>>>> abf4fbc657532dbe8f302d9ce2d78dbd2a009b82
	$(Q)$(MAKE) $(build)=gpio-hammer
$(OUTPUT)gpio-hammer: $(GPIO_HAMMER_IN)
	$(QUIET_LINK)$(CC) $(CFLAGS) $(LDFLAGS) $< -o $@

#
# gpio-event-mon
#
GPIO_EVENT_MON_IN := $(OUTPUT)gpio-event-mon-in.o
<<<<<<< HEAD
$(GPIO_EVENT_MON_IN): prepare FORCE
=======
$(GPIO_EVENT_MON_IN): prepare FORCE $(OUTPUT)gpio-utils-in.o
>>>>>>> abf4fbc657532dbe8f302d9ce2d78dbd2a009b82
	$(Q)$(MAKE) $(build)=gpio-event-mon
$(OUTPUT)gpio-event-mon: $(GPIO_EVENT_MON_IN)
	$(QUIET_LINK)$(CC) $(CFLAGS) $(LDFLAGS) $< -o $@

clean:
	rm -f $(ALL_PROGRAMS)
	rm -f $(OUTPUT)include/linux/gpio.h
	find $(if $(OUTPUT),$(OUTPUT),.) -name '*.o' -delete -o -name '\.*.d' -delete

install: $(ALL_PROGRAMS)
	install -d -m 755 $(DESTDIR)$(bindir);		\
	for program in $(ALL_PROGRAMS); do		\
		install $$program $(DESTDIR)$(bindir);	\
	done

FORCE:

.PHONY: all install clean FORCE prepare
