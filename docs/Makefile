DOCS_DIR:=$(dir $(abspath $(lastword $(MAKEFILE_LIST))))
PROJ_DIR:=$(shell cd $(DOCS_DIR)/.. && pwd)
# Minimal makefile for Sphinx documentation
#

# You can set these variables from the command line, and also
# from the environment for the first two.
PYTHON ?= $(PROJ_DIR)/packages/python/bin/python
SPHINXOPTS    ?=
SPHINXBUILD   ?= $(PROJ_DIR)/packages/python/bin/sphinx-build
SOURCEDIR     = .
BUILDDIR      = _build

# Put it first so that "make" without argument is like "make help".
help:
	@$(SPHINXBUILD) -M help "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

.PHONY: help Makefile

# Catch-all target: route all unknown targets to Sphinx using the new
# "make mode" option.  $(O) is meant as a shortcut for $(SPHINXOPTS).
%: Makefile $(DOCS_DIR)/$(BUILDDIR)/flow.dv.schema.json
	@$(SPHINXBUILD) -M $@ "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

$(DOCS_DIR)/$(BUILDDIR)/flow.dv.schema.json:
	mkdir -p $(dir $@)
	$(PYTHON) -m dv_flow.mgr.util schema -o $@
