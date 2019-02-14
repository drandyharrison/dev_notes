% Notes on using Pandoc

To create HTML from mardown, run to following command in command prompt:

```
	pandoc test1.md -f markdown -t html -s -o test1.html
```
	
The filename `test1.md` tells pandoc which file to convert. The `-s` option says to create a "_standalone_" file, with a header and footer, not just a fragment. And the `-o test1.html` says to put the output in the file `test1.html`. Note that we could have omitted `-f markdown` and `-t html`, since the default is to convert from markdown to HTML, but it doesn’t hurt to include them.

**Note**: double indent to ident code.

To create a pdf using `pandoc`,

```
	pandoc xxx.md --pdf-engine=yyy -o zzz.pdf
```

where `xxx.md` is the source markdown file, `yyy` is one of 

```
	wkhtmltopdf, weasyprint, prince, pdflatex, lualatex, 
	xelatex, pdfroff, context
````

and `zzz.pdf` is the output pdf file. For simple markdown and quick conversion `pdflatex` seems the best.

Synatx highlighting styles using `--highlight-style=pygments|kate|monchrome|
espresso|haddock|tango|zenburn|breezedark`

```
	pandoc syntax.md -s --highlight-style=breezedark
	--pdf-engine=pdflatex -o syntax.pdf
```

Default option is pygments, best one is breezedark. Dark backgrounds are espresso, zenburn and breezedark. Light grey background, tango.