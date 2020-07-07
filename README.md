# Template Ph.D. Biology U. de Sherbrooke (2020)
## Introduction
This template has not yet been validated. Because I am using a lot of tikz pictures, I use the compiler lualatex. It shall not change anything to you, except that the command line:
```zsh
	pdflatex myDoc.tex
```
is replaced by
```zsh
	lualatex myDoc.tex
```
Lualatex has also many other advantages, see https://ctan.org/pkg/lualatex-doc. Note that by changing few packages (polyglossia for instance) and few options, you can easily get back to ```pdflatex```

## Comments
Most of these comments are in the main.tex file. I just copy-paste them for ease of read
1. To stop numbering the lines, deactivate ```\linenumbers``` (activated after loading the package lineno)
2. To make the index, you need to compile first with ```lualatex``` (or ```pdflatex``` if you modified the template) and then use ```makeindex```. Example:
	```zsh
	lualatex main.tex
	makeindex main.nlo -s nomencl.ist -o main.nls
	lualatex main.tex
	```
3. For the bibliography, use the command ```biber``` (as I am using the package biblatex, much more modern than bibtex).
	To use multiple bibliography, use the ```refsection environment``` (3.13.3 Multiple Bibliographies in biblatex doc Version 3.13). Do not use the chapterbib package with biblatex, there is refsection environment for that!
	Each article will need to use:
	```latex
	\begin{refsection}
		Blablabla articles
		\printbibliography[heading=subbibnumbered]
	\end{refsection}
	```
	For the introduction and discussion, do not use the ```\refsection``` environment as the bibliographies have to be together, neither do use ```\printbibliography[heading=subbibnumbered]```. All the citations of the intro and discussion will be cited at the end with the command
	```latex
		\printbibliography[heading=bibintoc, title=BIBLIOGRAPHIE]
	```
4. I defined two languages in the document, French and British english (which is the main language), use \begin{french} ... \end{french} to switch to French in a paragraph
5. To avoid multi-defined labels, I recommend to apply this command line in your shell for each tex file of the folders ./article1/, ./article2/, ...:
	```zsh
		sed -i.tmp 's/\\label{/\\label{WHATEVER::/g' *.tex
	```
	This will change all the labels by adding WHATEVER before. Example (adding article1 for each tex file in ./article1/ folder), \label{sec::intro} in ./article1/chap1.tex becomes \label{article1::sec::intro}. Similarily, you can change all the refs by adding WHATEVER before with the command
	```zsh
		sed -i.tmp 's/\\ref{/\\ref{WHATEVER::/g' *.tex
	```
	Example (adding article1 for each tex file in ./article1/ folder): \ref{sec::intro} in ./article1/chap1.tex becomes \ref{article1::sec::intro}. You got, it, you can do it for ``` \eqref{} ``` too, and for any other label you need that could create conflicts between your chapters written independently.
	```zsh
		sed -i.tmp 's/\\eqref{/\\eqref{WHATEVER::/g' *.tex
	```
	This will change all the eqrefs by adding WHATEVER before. Example (adding article1 for each tex file in ./article1/ folder): \eqref{eq::R0_equation} in ./article1/chap1.tex becomes \eqref{article1::eq::R0_equation}. For safety reasons, the original file will be kept in a temporary file '.tmp'. Example:
	```zsh
		sed -i.tmp 'Your instructions here' introduction.tex
	```
	will create two files:

		- introduction.tex which should be the one to keep (if no mistakes in the sed instructions)
		- introduction.tex.tmp which is the original file (that you can dump if sed behaved the way you expected)
	
	For an introduction to the power of sed and regular expressions: https://www.grymoire.com/Unix/Sed.html#uh-1 
6. I defined some colours in this document. Except RdeepBlue, none of them is used in this template and can be deleted.
 	If you delete RdeepBlue, do not forget to adapt all the commands using this colour!