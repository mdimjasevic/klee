#===-- runtime/musl/Makefile --------------------------*- Makefile -*--========#
#
#                     The KLEE Symbolic Virtual Machine
#
# This file is distributed under the University of Illinois Open Source
# License. See LICENSE.TXT for details.
#
#===------------------------------------------------------------------------===#

# Note musl does not really live here.  This makefile just manages the
# location of the musl bitcode archive when building and when
# installing KLEE.

LEVEL=../..

# We're not really building a bytecode library here but we need to set
# this so that $(BuildMode) is set appropriately
BYTECODE_LIBRARY=1

include $(LEVEL)/Makefile.common

# The purpose of setting up this symbolic link is so that KLEE can
# always look for musl in the same place it looks for all the other
# run time libraries
musl_symlink:=$(PROJ_OBJ_ROOT)/$(BuildMode)/lib/$(MUSL_BCA_NAME)
#
# Force our extra rules to run
all-local:: $(musl_symlink)

$(musl_symlink):
	@echo "Setting up symbolic link to musl"
	-$(Verb) $(MKDIR) $(PROJ_OBJ_ROOT)/$(BuildMode)/lib
	$(Verb) ln -s -f $(MUSL_BCA) $(musl_symlink)

# The reasons for copying over musl on install are
#
# * KLEE can look for musl in the same place it looks for all other run
#   time libraries. 
# * KLEE can be more easily distributed with musl

install:: copy_musl
uninstall:: remove_musl

.PHONY: copy_musl remove_musl

copy_musl:
	@echo "Installing musl archive"
	$(Verb) $(CP) $(MUSL_BCA) $(BYTECODE_DESTINATION)/$(MUSL_BCA_NAME)

remove_musl:
	@echo "Removing musl archive"
	$(Verb) $(RM) $(BYTECODE_DESTINATION)/$(MUSL_BCA_NAME)
