BOOK=book

all:
	pdflatex ${BOOK}.tex
	pdflatex ${BOOK}.tex
	pdflatex ${BOOK}.tex

clean:
	rm -f ${BOOK}.aux
	rm -f ${BOOK}.log

squeaky: clean
	rm -f ${BOOK}.pdf
