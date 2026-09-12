# Informe/memoria UC3M. Requiere lualatex + latexmk + Montserrat.
MAIN := main
OUT  := build

.PHONY: all clean

all:
	latexmk -lualatex -interaction=nonstopmode -halt-on-error \
	        -outdir=$(OUT) $(MAIN).tex

clean:
	latexmk -lualatex -C -outdir=$(OUT) $(MAIN).tex
	rm -rf $(OUT)
