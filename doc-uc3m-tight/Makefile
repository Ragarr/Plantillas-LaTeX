# Plantilla comprimida UC3M. Requiere lualatex + latexmk + Montserrat.
# Genera tres PDF de demo: a una columna (main.pdf), a dos columnas
# (main-twocolumn.pdf) y la version en ingles (main-en.pdf).
DOCS := main main-twocolumn main-en
OUT  := build

.PHONY: all clean

all:
	@for doc in $(DOCS); do \
	  latexmk -lualatex -interaction=nonstopmode -halt-on-error \
	          -outdir=$(OUT) $$doc.tex || exit 1; \
	done

clean:
	rm -rf $(OUT)
