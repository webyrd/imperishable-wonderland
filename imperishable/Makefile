BOOK=book

all:
	pandoc -f markdown -t pdf ${BOOK}.md -o ${BOOK}.pdf

squeaky: clean
	rm -f ${BOOK}.pdf
