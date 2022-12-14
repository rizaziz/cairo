include $(top_srcdir)/build/Makefile.am.common
include $(top_srcdir)/src/Makefile.am.features

# The name of the module.
DOC_MODULE=cairo

# The top-level SGML file.
DOC_MAIN_SGML_FILE=cairo-docs.xml

# Extra options to supply to gtkdoc-scan
SCAN_OPTIONS=--deprecated-guards="CAIRO_DISABLE_DEPRECATED" --ignore-decorators="cairo_public|cairo_private"

# The directory containing the source code.
DOC_SOURCE_DIR=$(top_srcdir)/src

# Used for dependencies
HFILE_GLOB=$(top_srcdir)/src/cairo*.h
CFILE_GLOB=$(top_srcdir)/src/cairo*.c
EXTRA_HFILES=$(top_builddir)/src/cairo-supported-features.h

# Headers to ignore
IGNORE_HFILES= \
	cairo-features.h \
	cairo-features-win32.h \
	$(all_cairo_private) \
	$(unsupported_cairo_headers) \
	$(NULL)

# Extra options to supply to gtkdoc-mkdb
MKDB_OPTIONS=--sgml-mode --output-format=xml --name-space=cairo

# Non-autogenerated SGML files to be included in $(DOC_MAIN_SGML_FILE)
content_files =	\
	language-bindings.xml \
	version.xml \
	$(NULL)

version.xml: $(top_srcdir)/src/cairo-version.h
	echo $(CAIRO_VERSION_MAJOR).$(CAIRO_VERSION_MINOR).$(CAIRO_VERSION_MICRO) > $@

# Images to copy into HTML directory
HTML_IMAGES =

# Extra options to supply to gtkdoc-fixref
FIXXREF_OPTIONS=

include $(top_srcdir)/build/Makefile.am.gtk-doc

dist-hook: doc

# This line really belongs in gtk-doc.mk
$(REPORT_FILES): sgml-build.stamp

if ENABLE_GTK_DOC
TESTS += check-doc-coverage.sh
endif

TESTS += check-doc-syntax.sh
EXTRA_DIST += check-doc-coverage.sh check-doc-syntax.sh
TESTS_ENVIRONMENT = srcdir="$(srcdir)" top_srcdir="$(top_srcdir)" MAKE="$(MAKE) $(AM_MAKEFLAGS)" DOC_MODULE="$(DOC_MODULE)" REPORT_FILES="$(REPORT_FILES)"
