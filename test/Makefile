
v1.19 = 1.19.1
v1.18 = 1.18
v1.17 = 1.17.2
v1.16 = 1.16.0.2
v1.15 = 1.15.2

PANDOC-1.19 = pandoc-$(v1.19)
PANDOC-1.18 = pandoc-$(v1.18)
PANDOC-1.17 = pandoc-$(v1.17)
PANDOC-1.16 = pandoc-$(v1.16)
PANDOC-1.15 = pandoc-$(v1.15)

PYTHON-2.7 = python2.7
PYTHON-3.4 = python3.4

PDFFLAGS = --variable geometry:margin=1in --standalone --variable urlcolor=blue
HTMLFLAGS = --standalone --variable urlcolor=blue


all: pdf html docx

pdf: out/test-1.19.pdf \
     out/test-1.19-py2.7.pdf \
     out/test-1.19-py3.4.pdf \
     out/test-1.19-cleveref.pdf \
     out/test-1.18.pdf \
     out/test-1.17.pdf \
     out/test-1.16.pdf \
     out/test-1.15.pdf

html: out/test-1.19.html

docx: out/test-1.19.docx


out/test-%.html: test.md
	@if [ ! -d $(dir $@) ]; then mkdir -p $(dir $@); fi
	$(PANDOC-$*) $< --filter pandoc-tablenos $(HTMLFLAGS) -o $@

out/test-%-py2.7.pdf: test.md
	@if [ ! -d $(dir $@) ]; then mkdir -p $(dir $@); fi
	$(PANDOC-$*) $< -t json | $(PYTHON-2.7) ../pandoc_tablenos.py latex --pandocversion=$(v$*) | $(PANDOC-$*) -f json $(PDFFLAGS) -o $@

out/test-%-py3.4.pdf: test.md
	@if [ ! -d $(dir $@) ]; then mkdir -p $(dir $@); fi
	$(PANDOC-$*) $< -t json | $(PYTHON-3.4) ../pandoc_tablenos.py latex --pandocversion=$(v$*) | $(PANDOC-$*) -f json $(PDFFLAGS) -o $@

out/test-%-cleveref.pdf: test.md
	@if [ ! -d $(dir $@) ]; then mkdir -p $(dir $@); fi
	$(PANDOC-$*) $< --filter pandoc-tablenos $(PDFFLAGS) --include-in-header=cleveref.tex -o $@

out/test-%.pdf: test.md
	@if [ ! -d $(dir $@) ]; then mkdir -p $(dir $@); fi
	$(PANDOC-$*) $< --filter pandoc-tablenos $(PDFFLAGS) -o $@

out/test-%.docx: test.md
	@if [ ! -d $(dir $@) ]; then mkdir -p $(dir $@); fi
	$(PANDOC-$*) $< --filter pandoc-tablenos -o $@


.PHONY: clean

clean:
	rm -rf out
