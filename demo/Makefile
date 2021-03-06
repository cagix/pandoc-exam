# Author: Carsten Gips <carsten.gips@fh-bielefeld.de>
# Copyright: (c) 2016 Carsten Gips
# License: MIT



## Path to pandoc templates/includes and language settings

DATADIR   = /home/cagix/.pandoc/
PREFIX    = ${DATADIR}/exam/
TEMPLATES = ${DATADIR}/templates/



## Source file and lecture prefix

# Files as defined in Excel sheet
XLS    = bla.md blub.md wuppie.md fluppie.md

SRC    = $(addprefix md/, $(XLS))

PDF    = exam.pdf solution.pdf
TMP1   = __header.filled.tex
TMP2   = __titlepage.filled.tex



## Exam options

PDFOPTIONS  = -f markdown --latex-engine=xelatex
#PDFOPTIONS += --template=${TEMPLATES}/default.latex
PDFOPTIONS += --default-image-extension=pdf
PDFOPTIONS += -V documentclass=exam -V classoption=addpoints
PDFOPTIONS += -V fontsize=11pt -V papersize=a4
PDFOPTIONS += -V geometry:left=2cm -V geometry:right=2cm -V geometry:top=2cm -V geometry:bottom=2.5cm
PDFOPTIONS += --standalone --smart --number-sections
PDFOPTIONS += --include-in-header=${PREFIX}/exam.tex
PDFOPTIONS += --include-in-header=${TMP1}
PDFOPTIONS += --include-before-body=${TMP2}
PDFOPTIONS += --include-before-body=${PREFIX}/exam_begin.tex
PDFOPTIONS += --include-after-body=${PREFIX}/exam_end.tex
PDFOPTIONS += --listings --highlight-style=tango
PDFOPTIONS += --toc  # to compile twice
PDFOPTIONS += --data-dir=${DATADIR}



## Targets

all:	$(PDF)

pdf:	clean $(PDF)


solution.pdf: PDFOPTIONS += -V classoption=answers
exam.pdf solution.pdf: metadata.yaml $(SRC) ${PREFIX}/header.tex ${PREFIX}/titlepage.tex
	pandoc --standalone --template=${PREFIX}/header.tex -o ${TMP1} metadata.yaml
	pandoc --standalone --template=${PREFIX}/titlepage.tex -o ${TMP2} metadata.yaml
	pandoc ${PDFOPTIONS} -o $@ $(SRC) metadata.yaml
	rm -f ${TMP1} ${TMP2}


clean:
	rm -f $(PDF) ${TMP1} ${TMP2}


.PHONY: clean




