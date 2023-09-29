TEX_ENGINE = xelatex
BIBTEX_ENGINE = biblatex
TEST_FILE := report.pdf

all: config $(TEST_FILE)

.PHONY: all clean config debug test .FORCE

debug: clean config
	$(TEX_ENGINE) $(basename $(TEST_FILE)).tex
	$(TEX_ENGINE) $(basename $(TEST_FILE)).tex
	$(TEX_ENGINE) $(basename $(TEST_FILE)).tex

test: $(TEST_FILE)
	@printf "Opening %s\n" $(TEST_FILE)
	@code $(TEST_FILE)

%.pdf: %.tex config .FORCE
	@printf "Building 1/4\n"
	@timeout 10 $(TEX_ENGINE) $< >/dev/null
	@printf "\033[1K\033[1FBuilding 2/4\n"
	@timeout 10 $(BIBTEX_ENGINE) $<  >/dev/null
	@printf "\033[1K\033[1FBuilding 3/4\n"
	@timeout 10 $(TEX_ENGINE) $<  >/dev/null
	@printf "\033[1K\033[1FBuilding 4/4\n"
	@timeout 10 $(TEX_ENGINE) $<  >/dev/null
	@printf "\033[1;32m\033[1F\033[2KDone.\033[0m\n"

config:

clean:
	@echo "Cleaning things up"
	@rm -rf *.pdf *.aux *.bbl *.fdb_latexmk *.fls *.ind *.inx *.lof *.log *.lol *.lot *.out *.synctex.gz *.toc
