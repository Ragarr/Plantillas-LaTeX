# Informe/memoria UC3M. Requiere lualatex + latexmk + Montserrat + rsvg-convert
# + pdfcrop (para generar los logos PDF a partir de los SVG versionados).
MAIN := main
OUT  := build

LOGO_DIR    := logos
LOCKUP_SVG  := $(LOGO_DIR)/Acrónimo_y_nombre_de_la_UC3M.svg
SEAL_SVG    := $(LOGO_DIR)/Logo_UC3M.svg
LOCKUP_PDF  := $(LOGO_DIR)/logo-uc3m-lockup.pdf
SEAL_PDF    := $(LOGO_DIR)/logo-uc3m-seal.pdf
MARK_PDF    := $(LOGO_DIR)/logo-uc3m-mark.pdf
MARK_TMPSVG := $(LOGO_DIR)/.uc3m-mark-crop.svg
LOGOS       := $(LOCKUP_PDF) $(SEAL_PDF) $(MARK_PDF)

.PHONY: all clean

all: $(LOGOS)
	latexmk -lualatex -interaction=nonstopmode -halt-on-error \
	        -outdir=$(OUT) $(MAIN).tex

$(SEAL_PDF): $(SEAL_SVG)
	rsvg-convert -f pdf -o $@ "$<"
	pdfcrop --margins 2 $@ $@.tmp && mv $@.tmp $@

$(LOCKUP_PDF): $(LOCKUP_SVG)
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
