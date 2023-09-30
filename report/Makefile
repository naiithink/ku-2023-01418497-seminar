TEX_ENGINE = xelatex
TEX_ENGINE_OPT = --interaction batchmode
BIBTEX_ENGINE = bibtex
TEST_FILE := report.pdf

all: config $(TEST_FILE)

.PHONY: all clean config debug test .FORCE

debug: clean config
	$(TEX_ENGINE) $(basename $(TEST_FILE)).tex
	$(BIBTEX_ENGINE) $(basename $(TEST_FILE))
	$(TEX_ENGINE) $(basename $(TEST_FILE)).tex
	$(TEX_ENGINE) $(basename $(TEST_FILE)).tex

test: $(TEST_FILE)
	@printf "Opening %s\n" $(TEST_FILE)
	@code $(TEST_FILE)

%.pdf: %.tex config .FORCE
	@printf "Building 1/4\n"
	@timeout 10 $(TEX_ENGINE) $(TEX_ENGINE_OPT) $< >/dev/null
	@printf "\033[1K\033[1FBuilding 2/4\n"
	@timeout 10 $(BIBTEX_ENGINE) $<  >/dev/null
	@printf "\033[1K\033[1FBuilding 3/4\n"
	@timeout 10 $(TEX_ENGINE) $(TEX_ENGINE_OPT) $<  >/dev/null
	@printf "\033[1K\033[1FBuilding 4/4\n"
	@timeout 10 $(TEX_ENGINE) $(TEX_ENGINE_OPT) $<  >/dev/null
	@printf "\033[1;32m\033[1F\033[2KDone.\033[0m\n"

config:

clean:
	@echo "Cleaning things up"
	@rm -rf $(basename $(TEST_FILE)).pdf \
	$(basename $(TEST_FILE)).aux \
	$(basename $(TEST_FILE)).bbl \
	$(basename $(TEST_FILE)).blg \
	$(basename $(TEST_FILE))-blx.bib \
	$(basename $(TEST_FILE)).fdb_latexmk \
	$(basename $(TEST_FILE)).fls \
	$(basename $(TEST_FILE)).ind \
	$(basename $(TEST_FILE)).inx \
	$(basename $(TEST_FILE)).lof \
	$(basename $(TEST_FILE)).log \
	$(basename $(TEST_FILE)).lol \
	$(basename $(TEST_FILE)).lot \
	$(basename $(TEST_FILE)).out \
	$(basename $(TEST_FILE)).run.xml \
	$(basename $(TEST_FILE)).synctex.gz \
	$(basename $(TEST_FILE)).toc
