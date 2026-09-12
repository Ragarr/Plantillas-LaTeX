# Plantilla comprimida UC3M. Requiere lualatex + latexmk + Montserrat.
# Genera dos PDF de demo con el mismo contenido (content.tex): a una
# columna (main.pdf) y a dos columnas (main-twocolumn.pdf).
DOCS := main main-twocolumn
OUT  := build

.PHONY: all clean

all:
	@for doc in $(DOCS); do \
	  latexmk -lualatex -interaction=nonstopmode -halt-on-error \
	          -outdir=$(OUT) $$doc.tex || exit 1; \
	done

clean:
	rm -rf $(OUT)
