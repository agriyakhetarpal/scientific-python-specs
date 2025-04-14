PREVIEW_DEST:=$(if $(PREVIEW_DEST),$(PREVIEW_DEST),/tmp/__specs.scientific-python.org_site-preview)
HUGO_OPTS=--disableFastRender
OUTPUT_DIR:=dist

.PHONY: clean preview prepare-preview preview-serve preview-build
.DEFAULT_GOAL: preview-serve

# Substitute the SPECs in specs.scientific-python.org with
# those from this repository
prepare-preview: clean
	mkdir -p $(PREVIEW_DEST)
	git clone https://github.com/scientific-python/scientific-python.org $(PREVIEW_DEST)
	git -C $(PREVIEW_DEST) submodule set-url themes/scientific-python-hugo-theme https://github.com/scientific-python/scientific-python-hugo-theme.git
	git -C $(PREVIEW_DEST) submodule update --init
	rm -rf $(PREVIEW_DEST)/content/specs/*
	cp -r * $(PREVIEW_DEST)/content/specs

# Serve SPECs to http://localhost:1313
preview-serve: prepare-preview
	cd $(PREVIEW_DEST) && make serve

# Build website to dist/
preview-build: prepare-preview
	cd $(PREVIEW_DEST) && make html
	mkdir -p $(OUTPUT_DIR)
	cp -r $(PREVIEW_DEST)/public/* $(OUTPUT_DIR)/

clean:
	rm -rf $(PREVIEW_DEST)
	rm -rf $(OUTPUT_DIR)
