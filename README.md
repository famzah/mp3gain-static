This repository contains 32-bit and 64-bit static binary builds of [mp3gain](http://mp3gain.sourceforge.net/).

The static binaries let you use "mp3gain" without having to install any dependency libraries.

Build procedure on a Debian/Ubuntu system:

```Bash
apt-get source mp3gain

cd mp3gain-1.5.2-r2/

vi Makefile
	# CFLAGS+= -Wall -DHAVE_MEMCPY
	#   becomes
	# CFLAGS+= -Wall -DHAVE_MEMCPY -static -static-libgcc -static-libstdc++
	#
	# LIBS= -lm
	#   becomes
	# LIBS= -lm -static -static-libgcc -static-libstdc++

make   # compile statically
strip --strip-all mp3gain   # reduce size a bit

# some checks as advised at http://stackoverflow.com/a/15475134/198219

ldd mp3gain   # returns "not a dynamic executable"
nm mp3gain | grep " U "   # returns nothing
file mp3gain   # check on both our build platforms (the 32-bit and the 64-bit one)
	# ELF 32-bit LSB  executable, Intel 80386, version 1 (SYSV), statically linked, for GNU/Linux 2.6.24
	# ELF 64-bit LSB  executable, x86-64, version 1 (SYSV), statically linked, for GNU/Linux 2.6.24
```
