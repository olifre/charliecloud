# Bugs in this Makefile:
#
# 1. $(EXEEXT) not included for scripts.

## C programs

bin_PROGRAMS = ch-checkns ch-run ch-ssh

ch_checkns_SOURCES = ch-checkns.c ch_misc.h ch_misc.c

ch_run_SOURCES = ch-run.c ch_core.h ch_core.c ch_misc.h ch_misc.c
ch_run_CFLAGS = $(CFLAGS) $(PTHREAD_CFLAGS)
ch_run_LDADD = $(LIBRT)

ch_ssh_SOURCES = ch-ssh.c ch_misc.h ch_misc.c


## Shell scripts - distributed as-is

dist_bin_SCRIPTS = ch-build \
                   ch-build2dir \
                   ch-builder2squash \
                   ch-builder2tar \
                   ch-dir2squash \
                   ch-fromhost \
                   ch-mount \
                   ch-pull2dir \
                   ch-pull2tar \
                   ch-tar2dir \
                   ch-test \
                   ch-umount


## Python scripts - need text processing

bin_SCRIPTS = ch-run-oci  # scripts to build
EXTRA_SCRIPTS = ch-image  # more scripts that *may* be built
if ENABLE_CH_IMAGE
bin_SCRIPTS += ch-image
endif
EXTRA_DIST = ch-image.py.in ch-run-oci.py.in
CLEANFILES = $(bin_SCRIPTS) $(EXTRA_SCRIPTS)

ch-image: ch-image.py.in
ch-run-oci: ch-run-oci.py.in

$(bin_SCRIPTS): %: %.py.in
	rm -f $@
	sed -E 's|%PYTHON_SHEBANG%|@PYTHON_SHEBANG@|' < $< > $@
	chmod +rx,-w $@  # respects umask
