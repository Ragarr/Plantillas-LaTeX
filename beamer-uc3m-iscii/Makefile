# Presentación UC3M-ISCIII. Requiere lualatex + latexmk + Montserrat.
# Genera dos PDF de demo: en español (main.pdf) y en inglés (main-en.pdf).
DOCS := main main-en
OUT  := build

.PHONY: all clean

all:
	@for doc in $(DOCS); do \
	  latexmk -lualatex -interaction=nonstopmode -halt-on-error \
	          -outdir=$(OUT) $$doc.tex || exit 1; \
	done

clean:
	rm -rf $(OUT)
