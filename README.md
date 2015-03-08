Texprlcount
===========

texprlcount is a Perl script that uses texcount to estimate the word count for Physical Review Letters articles (or other Physical Review articles).

APS sets a limit of 3500 words for PRL articles and provides a guide for estimating the length of a paper:

https://journals.aps.org/authors/length-guide

This script uses the output of texcount to evaluate the word count by considering:

* words in text
* words in captions
* inline equations (1 equation = 1 word)
* displayed equation (1 equation = 12 words)

and excluding

* bibliography
* title and abstract (if .tex file is conveniently edited)
* acknowledgements (like above)

Then, it detects the images appearing in the document and their aspect ratio, based on the output log of pdflatex.

Instructions
------------
In order to use texprlcount, do the following

* Make sure that texcount is installed (most tex distributions include it)
* Tell texcount which parts of the document must be excluded by wrapping the part between the following two comments:

    %TC:ignore ... %TC:endignore
	
  For example, the abstract and acknowledgements must be excluded from the word count:
  
  	%TC:ignore
	\begin{abstract}
		...
	\end{abstract}
	%TC:endignore

* Compile the document with `pdflatex`. Do not delete the `.log` file.
* Use texprlcount with the following syntax

    texprlcount filename.tex

* Manually handle the situations that are currently not handled by texprlcount

NOTE
----

texprlcount is offered as a tool for estimating the word count of a tex document. texprlcount may fail to produce the correct estimation for a number of reasons and should be used with caution.

In particular, please note the following

* A number of features are still missing (see below)
* Embedded graphics, such as tikz code, are not recognized

Missing features
----------------
* Word count for tables
* Detect single/two-column figures
* Detect single/two-column equations and aligns