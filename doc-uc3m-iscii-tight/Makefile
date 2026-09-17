# Plantilla comprimida UC3M + ISCIII. Requiere lualatex + latexmk +
# Montserrat + rsvg-convert + pdfcrop (para generar los logos PDF a partir
# de los SVG versionados). Genera tres PDF de demo: a una columna
# (main.pdf), a dos columnas (main-twocolumn.pdf) y la version en ingles
# (main-en.pdf).
DOCS := main main-twocolumn main-en
OUT  := build

LOGO_DIR    := logos
LOCKUP_SVG  := $(LOGO_DIR)/Acrónimo_y_nombre_de_la_UC3M.svg
ISCIII_SVG  := $(LOGO_DIR)/logo-isciii.svg
MARK_PDF    := $(LOGO_DIR)/logo-uc3m-mark.pdf
ISCIII_PDF  := $(LOGO_DIR)/logo-isciii.pdf
MARK_TMPSVG := $(LOGO_DIR)/.uc3m-mark-crop.svg
LOGOS       := $(MARK_PDF) $(ISCIII_PDF)

.PHONY: all clean

all: $(LOGOS)
	@for doc in $(DOCS); do \
	  latexmk -lualatex -interaction=nonstopmode -halt-on-error \
	          -outdir=$(OUT) $$doc.tex || exit 1; \
	done

$(ISCIII_PDF): $(ISCIII_SVG)
	rsvg-convert -f pdf -o $@ "$<"
	pdfcrop --margins 2 $@ $@.tmp && mv $@.tmp $@

# Marca sola ("uc3m"): recorta el viewBox del lockup justo antes de la barra
# separadora (rect x="353.3" en el SVG original), quedandose solo con la
# parte izquierda, sin "Universidad Carlos III de Madrid".
$(MARK_PDF): $(LOCKUP_SVG)
	sed 's/viewBox="0 0 842 303"/viewBox="0 0 350 303"/' "$<" > $(MARK_TMPSVG)
	rsvg-convert -f pdf -o $@ $(MARK_TMPSVG)
	pdfcrop --margins 2 $@ $@.tmp && mv $@.tmp $@
	rm -f $(MARK_TMPSVG)

clean:
	rm -rf $(OUT)
	rm -f $(LOGOS) $(MARK_TMPSVG)
