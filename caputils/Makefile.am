# Makefile.am
# Automake file for the "capture utilities" routines for Wireshark
#
# Wireshark - Network traffic analyzer
# By Gerald Combs <gerald@wireshark.org>
# Copyright 1998 Gerald Combs
#
# This program is free software; you can redistribute it and/or
# modify it under the terms of the GNU General Public License
# as published by the Free Software Foundation; either version 2
# of the License, or (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.

include $(top_srcdir)/Makefile.am.inc

AM_CPPFLAGS = $(INCLUDEDIRS) $(WS_CPPFLAGS) $(GLIB_CFLAGS) $(PCAP_CFLAGS) \
		$(LIBNL_CFLAGS)

noinst_LIBRARIES = libcaputils.a

# All sources that should be put in the source distribution tarball
libcaputils_a_SOURCES = \
	capture_ifinfo.h		\
	capture-pcap-util.h		\
	capture-pcap-util.c		\
	capture-pcap-util-unix.c	\
	capture-pcap-util-int.h		\
	capture-wpcap.h			\
	capture_wpcap_packet.h		\
	iface_monitor.c			\
	iface_monitor.h			\
	ws80211_utils.c			\
	ws80211_utils.h

#
# This is used to build dumpcap, and dumpcap is, if possible, built as
# a position-independent executable (for address space layout randomization,
# as it might be running with extra privileges), so this library needs
# to be built that way as well.
#
libcaputils_a_CFLAGS = $(AM_CFLAGS) $(PIE_CFLAGS)

libcaputils_a_DEPENDENCIES =

CLEANFILES = \
	doxygen-caputils.tag

EXTRA_DIST = \
	.editorconfig		\
	airpcap.h		\
	airpcap_loader.c	\
	airpcap_loader.h	\
	capture_win_ifnames.c	\
	capture_win_ifnames.h	\
	capture-wpcap.c		\
	capture-wpcap.h		\
	capture_wpcap_packet.c  \
	capture_wpcap_packet.h  \
	CMakeLists.txt		\
	doxygen.cfg.in

doxygen:
if HAVE_DOXYGEN
	$(DOXYGEN) doxygen.cfg
endif		# HAVE_DOXYGEN

wsar_html: doxygen.cfg ../doxygen_global.cfg
if HAVE_DOXYGEN
	(umask 022 ; $(DOXYGEN) doxygen.cfg)
endif

checkapi: checkapi-base checkapi-todo

checkapi-base:
	$(PERL) $(top_srcdir)/tools/checkAPIs.pl -g deprecated-gtk -build \
	-sourcedir=$(srcdir) \
	$(libcaputils_a_SOURCES)

checkapi-todo:
	$(PERL) $(top_srcdir)/tools/checkAPIs.pl -M -g deprecated-gtk-todo -build \
	-sourcedir=$(srcdir) \
	$(libcaputils_a_SOURCES)
