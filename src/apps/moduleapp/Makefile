# === UCSF ChimeraX Copyright ===
# Copyright 2022 Regents of the University of California. All rights reserved.
# This software is provided pursuant to the ChimeraX license agreement, which
# covers academic and commercial uses. For more information, see
# <https://www.rbvi.ucsf.edu/chimerax/docs/licensing.html>
#
# This file is part of the ChimeraX library. You can also redistribute and/or
# modify it under the GNU Lesser General Public License version 2.1 as
# published by the Free Software Foundation. For more details, see
# <https://www.gnu.org/licenses/old-licenses/lgpl-2.1.html>
#
# This file is distributed WITHOUT ANY WARRANTY; without even the implied
# warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. This notice
# must be embedded in or attached to all copies, including partial copies, of
# the software or any revisions or derivations thereof."""
# === UCSF ChimeraX Copyright ===

# module application
#
# Include this Makefile and set MOD_NAME to the name of the
# chimerax module for the application.  bin/MOD_NAME will be
# the application and it invoke the chimerax.MOD_NAME module.
# (APP_NAME is set in config.make.)

TOP = ../../..
include $(TOP)/mk/config.make

#MOD_NAME = 
PKG_DIR = $(PYSITEDIR)/chimerax
APP_PKG_DIR = $(APP_PYSITEDIR)/chimerax
ifeq ($(OS),Darwin)
	OS_BIN = MacOS
else
	OS_BIN = bin
endif

all: $(MOD_NAME).sh

install: all
	SUFFIX=""; \
	if [ ! -d $(MOD_NAME) ]; then \
		SUFFIX=".py"; \
	fi; \
	if [ -f $(MOD_NAME)$$SUFFIX ]; then \
		$(RSYNC) $(MOD_NAME)$$SUFFIX $(PKG_DIR); \
	fi; \
	$(RSYNC) $(MOD_NAME).sh $(bindir)/$(MOD_NAME); \
	if [ -d "$(app_prefix)" ]; then \
		if [ -f $(MOD_NAME)$$SUFFIX ]; then \
			$(RSYNC) $(MOD_NAME)$$SUFFIX $(APP_PKG_DIR); \
		fi; \
		$(RSYNC) $(MOD_NAME).sh $(app_bindir)/$(MOD_NAME); \
	fi

clean:
	rm -f $(MOD_NAME).sh

pylint:
	$(PYLINT) $(MOD_NAME).py

$(MOD_NAME).sh: ../moduleapp/mod_app.sh.in
	sed -e 's,APP_NAME,$(APP_NAME),' \
		-e 's,OS_BIN,$(OS_BIN),' \
		-e 's,MOD_NAME,$(MOD_NAME),' \
		< ../moduleapp/mod_app.sh.in > $(MOD_NAME).sh
	chmod +x $(MOD_NAME).sh
