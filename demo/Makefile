

## Path to pandoc templates/includes and language settings

DATADIR = /home/cagix/.pandoc/
PREFIX  = ${DATADIR}/exam/

LANG    = -V lang=de-DE -M lang=de-DE



## Source file and lecture prefix

SRC    = $(addprefix md/, bla.md blub.md wuppie.md fluppie.md)

PDF    = klausur.pdf muster.pdf
TMP1   = __header.filled.tex
TMP2   = __titlepage.filled.tex



## Exam options

PDFOPTIONS  = -f markdown --latex-engine=xelatex
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
PDFOPTIONS += ${LANG} --data-dir=${DATADIR}



## Targets

all:	$(PDF) 

pdf:	clean $(PDF)


klausur.pdf: klausur.md $(SRC) ${PREFIX}/header.tex ${PREFIX}/titlepage.tex
	pandoc --standalone --template ${PREFIX}/header.tex -o ${TMP1} klausur.md
	pandoc --standalone --template ${PREFIX}/titlepage.tex -o ${TMP2} klausur.md
	pandoc ${PDFOPTIONS} -o $@ klausur.md $(SRC)
	rm -f ${TMP1} ${TMP2}

muster.pdf: klausur.md $(SRC) ${PREFIX}/header.tex ${PREFIX}/titlepage.tex
	pandoc --standalone --template ${PREFIX}/header.tex -o ${TMP1} klausur.md
	pandoc --standalone --template ${PREFIX}/titlepage.tex -o ${TMP2} klausur.md
	pandoc ${PDFOPTIONS} -V classoption=answers -o $@ klausur.md $(SRC)
	rm -f ${TMP1} ${TMP2}


clean:
	rm -f $(PDF) ${TMP1} ${TMP2}


.PHONY: clean



