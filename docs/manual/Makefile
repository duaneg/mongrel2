JUNK_FILES=book-final.* *.aux *.log styles/*.aux
SOURCE=book
WEBSITE=$(USER)@mongrel2.org:deployment/files/static
FINAL=book-final

draft: book-final.dvi
	htlatex book-final.tex
	tidy -quiet -ashtml -omit -ic -m book-final.html || true

book-final.dvi:
	cp $(SOURCE).tex book-final.tex
	latex -halt-on-error book-final.tex

book-final.pdf: book-final.dvi
	dvipdf book-final.dvi

view: book-final.pdf
	evince book-final.pdf

clean:
	rm -rf $(JUNK_FILES)
	find . -name "*.aux" -exec rm {} \;

release: clean book-final.pdf draft book-final.pdf sync

sync:
	rsync -vz $(FINAL).pdf $(WEBSITE)/mongrel2-manual.pdf
	rsync -vz $(FINAL).html $(WEBSITE)/mongrel2-manual.html
	rsync -vz $(FINAL).css $(FINAL)[0-9]*.html $(WEBSITE)/ 

