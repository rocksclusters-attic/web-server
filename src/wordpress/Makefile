#
# $Id: Makefile,v 1.20 2012/11/27 00:49:37 phil Exp $
#
# @Copyright@
# 
# 				Rocks(r)
# 		         www.rocksclusters.org
# 		         version 5.6 (Emerald Boa)
# 		         version 6.1 (Emerald Boa)
# 
# Copyright (c) 2000 - 2013 The Regents of the University of California.
# All rights reserved.	
# 
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions are
# met:
# 
# 1. Redistributions of source code must retain the above copyright
# notice, this list of conditions and the following disclaimer.
# 
# 2. Redistributions in binary form must reproduce the above copyright
# notice unmodified and in its entirety, this list of conditions and the
# following disclaimer in the documentation and/or other materials provided 
# with the distribution.
# 
# 3. All advertising and press materials, printed or electronic, mentioning
# features or use of this software must display the following acknowledgement: 
# 
# 	"This product includes software developed by the Rocks(r)
# 	Cluster Group at the San Diego Supercomputer Center at the
# 	University of California, San Diego and its contributors."
# 
# 4. Except as permitted for the purposes of acknowledgment in paragraph 3,
# neither the name or logo of this software nor the names of its
# authors may be used to endorse or promote products derived from this
# software without specific prior written permission.  The name of the
# software includes the following terms, and any derivatives thereof:
# "Rocks", "Rocks Clusters", and "Avalanche Installer".  For licensing of 
# the associated name, interested parties should contact Technology 
# Transfer & Intellectual Property Services, University of California, 
# San Diego, 9500 Gilman Drive, Mail Code 0910, La Jolla, CA 92093-0910, 
# Ph: (858) 534-5815, FAX: (858) 534-7345, E-MAIL:invent@ucsd.edu
# 
# THIS SOFTWARE IS PROVIDED BY THE REGENTS AND CONTRIBUTORS ``AS IS''
# AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
# THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
# PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE REGENTS OR CONTRIBUTORS
# BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
# CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
# SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR
# BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
# WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE
# OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN
# IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
# 
# @Copyright@
#
# $Log: Makefile,v $
# Revision 1.20  2012/11/27 00:49:37  phil
# Copyright Storm for Emerald Boa
#
# Revision 1.19  2012/05/06 05:49:48  phil
# Copyright Storm for Mamba
#
# Revision 1.18  2011/07/23 02:31:41  phil
# Viper Copyright
#
# Revision 1.17  2011/05/02 20:48:58  phil
# Add an uploads directory so that some standard wp functions can complete
# when editing a site interactively.
#
# Revision 1.16  2011/05/01 02:54:51  phil
# Updated Wordpress.
# New theme for cluster web site
#
# Revision 1.15  2010/09/07 23:53:31  bruno
# star power for gb
#
# Revision 1.14  2010/08/25 22:26:29  bruno
# refresh for 5.4 beta
#
# Revision 1.13  2009/05/01 19:07:33  mjk
# chimi con queso
#
# Revision 1.12  2008/10/18 00:56:22  mjk
# copyright 5.1
#
# Revision 1.11  2008/06/11 19:08:10  bruno
# katz instructed me to -- because you should do what mason instructs
# you to do and then see what happens.
#
# Revision 1.10  2008/03/06 23:42:03  mjk
# copyright storm on
#
# Revision 1.9  2007/06/23 04:04:07  mjk
# mars hill copyright
#
# Revision 1.8  2006/12/02 01:04:59  anoop
# Ridiculously big ass commit.
# Also known as the week after thanksgiving 2006. Or "The day Anoop
# broke Rocks".
#
# Main Changes.
#
# 1. Added a roll-profile.mk file. This is meant as a makefile for building
# the profile rpm containing all the XML files meant for the roll. This is a
# breakaway from the spec.in file method of building the profile RPM.
#
# 2. The variable PWD is now changed to CURDIR. The main reason for this is
# PWD is supplied by the shell. CURDIR is the variable supplied by gmake itself.
# This means we can have a slightly more platform independant way of doing things.
# Also Solaris was failing to set PWD correctly in the source directories, wreaking
# havoc on the location of the BUILD and PKG directories.
#
# Revision 1.7  2006/09/11 22:50:45  mjk
# monkey face copyright
#
# Revision 1.6  2006/08/10 00:12:22  mjk
# 4.2 copyright
#
# Revision 1.5  2005/10/12 18:11:22  mjk
# final copyright for 4.1
#
# Revision 1.4  2005/09/16 01:05:01  mjk
# updated copyright
#
# Revision 1.3  2005/06/28 16:12:12  bruno
# touch up
#
# Revision 1.2  2005/06/28 16:11:27  bruno
# build wordpress from source so we can put all the files under
# /var/www/html/wordpress rather than /usr/share/wordpress
#
# Revision 1.1  2005/06/28 06:29:05  bruno
# the start of our new web site
#
#

PKGROOT		= /var/www/html/wordpress
REDHAT.ROOT     = $(CURDIR)/../../

HTTPDCONFD	= /etc/httpd/conf.d
CONFFILE	= rocks-wordpress.conf

-include $(ROCKSROOT)/etc/Rules.mk
include Rules.mk


build:
	gunzip -c $(NAME)-$(VERSION).tar.gz | $(TAR) -xf -
	(								\
		cd $(NAME);						\
	)
	

install::
	mkdir -p $(ROOT)/$(PKGROOT)
	(								\
		cd $(NAME);						\
		find . | cpio -pduv $(ROOT)/$(PKGROOT);			\
	)
	mkdir -p $(ROOT)/$(PKGROOT)/wpdb
	(								\
		cd wpdb_$(DBVERSION);					\
		find . | cpio -pduv $(ROOT)/$(PKGROOT)/wpdb;		\
	)
	mkdir -p $(ROOT)/$(HTTPDCONFD)
	install -m644 $(CONFFILE) $(ROOT)/$(HTTPDCONFD)
	if [ ! -d $(ROOT)/$(PKGROOT)/wp-content/themes/$(BASETHEME) ]; then \
		mkdir -p $(ROOT)/$(PKGROOT)/wp-content/themes/$(BASETHEME); fi
	cd $(BASETHEME); find . -name CVS -prune -o -print |  	\
		cpio -pduv $(ROOT)/$(PKGROOT)/wp-content/themes/$(BASETHEME)
	mkdir -p $(ROOT)/$(PKGROOT)/wp-content/uploads
	chmod 1777 $(ROOT)/$(PKGROOT)/wp-content/uploads


clean::
	rm -rf $(NAME)
	rm -f $(NAME).spec.in
