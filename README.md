# LaTeX Template for Review Responses

This repository is adapted from [Karl-Ludwig Besser's template](https://www.overleaf.com/latex/templates/review-response-template/tmbvmjstxwrd), which provides a simple LaTeX template for writing responses to reviewers. You may preview the PDF file [here](https://shellywhen.github.io/Journal-Response-Letter-Template-Latex/Review_Response_Template.pdf)

## Recent Updates

### Version 2.0 (January 2026)

**Major Improvements:**

1. **Bibliography System Migration**
   - Migrated from `biblatex+biber` to `natbib+bibtex` for better compatibility
   - Now uses `IEEEtran` bibliography style
   - Compilation workflow: `pdflatex → bibtex → pdflatex → pdflatex`

2. **Enhanced Cover Letter Layout**
   - Merged cover letter with title page for better space utilization
   - Added professional formatted table displaying manuscript information (Manuscript ID, Title, Authors)
   - Optimized spacing: 0.8cm above table, 0.3em table padding, 1.2em below horizontal rule

3. **Fixed General Comment Handling**
   - General comments no longer increment the comment counter
   - General responses now correctly labeled as "General Response:" (instead of "Response S0")
   - Proper indentation control with `\noindent` for consistent formatting

4. **Flexible Editor Command**
   - `\editor` command now accepts optional parameter for custom titles
   - Usage: `\editor[Associate Editor]` or `\editor[Action Editor]`
   - Default remains "Meta Review" for backward compatibility

5. **Visual Enhancements**
   - Added 3pt rounded corners to comment boxes for softer appearance
   - Applied drop fuzzy shadow effect for smooth gradient transitions
   - Improved typography with 2em paragraph indentation (English academic standard)

6. **Project Management**
   - Added comprehensive `.gitignore` file with 170+ LaTeX-specific patterns
   - Excludes auxiliary files (aux, log, bbl, blg, synctex, etc.)
   - PDF files allowed for template examples

**Bug Fixes:**
- Resolved `\citep` undefined control sequence error
- Fixed `\printpartbibliography` compatibility issues with bibtex
- Corrected comment numbering sequence (now starts correctly at 1.1 after general comments)

# Usage

In order to use the `reviewresponse.sty` package in your document, simply include the following line
in your LaTeX document
```latex
\usepackage[journal={Name of the Journal},
            manuscript={Number/ID of the Manuscript},
            editor={Name of the Editor}]{reviewresponse}
```

## Commands
The following commands are provided by the package.  
If you are using [TeXstudio](https://www.texstudio.org/), there exists an
autocomplete file (`.cwl`) for the `reviewresponse.sty` package, which can be
found [here](https://gist.github.com/klb2/29f6fffeac8cc79e3b3f79e980a6b9e3).

### Editor and Reviewers
```latex
\editor[optional title]
\reviewer
```
These commands start a new editor and reviewer.

**Editor Command:**
- Accepts optional parameter for custom title (new in v2.0)
- Examples: `\editor[Associate Editor]`, `\editor[Action Editor]`
- Default: `\editor` displays "Meta Review"

The typical usage is
```latex
\begin{document}
...
\editor
Response to the editor

\reviewer
Response to the first reviewer

\reviewer
Response to the second reviewer
```

### Comments and Responses
```latex
\begin{generalcomment}
...
\end{generalcomment}
```
The `generalcomment` environment is meant for general comments given by the
editor and reviewers. General comments do not increment the comment counter (fixed in v2.0), ensuring numbered comments start correctly at X.1.

**Response to General Comments:**
```latex
\begin{revmeta}[Optional Parameter]
...
\end{revmeta}
```
Use `revmeta` environment for responses to general comments. It displays as "General Response:" with proper formatting.



```latex
\begin{revcomment}
...
\end{revcomment}
```
The `revcomment` environment is meant for the individual comments made by the
reviewers.
They are automatically numbered.

It also accepts optional arguments, which are directly passed to the underlying
`tcolorbox` environment.
This is useful, if you want to add some arguments in specific situations, e.g.,
the `breakable` keyword for very long comments.


```latex
\begin{revresponse}[Optional Parameter]
...
\end{revresponse}
```
The `revresponse` environment is meant for responses to the individual comments
of the reviewers and editor.
The optional parameter changes the text on the first line.
By default, this text is "Thank you for the comment.".



### Changes
```latex
\begin{changes}
...
\end{changes}
```
The `changes` environment is meant for indicating changes that you made to your
manuscript.
It sets the content in a box in order to highlight it for the reviewers.


### Bibliography
The `reviewresponse` package now uses `natbib` for references (migrated from `biblatex` in v2.0).

**Setup:**
```latex
\usepackage[numbers,sort&compress]{natbib}
\bibliographystyle{IEEEtran}
...
\bibliography{literature}  % at the end of document
```

**Citation Commands:**
- Use `\citep{}` for parenthetical citations: (Author, Year)
- Use `\citet{}` for textual citations: Author (Year)
- Use `\cite{}` for numeric citations: [1]

**Compilation:**
```bash
pdflatex review_response.tex
bibtex review_response
pdflatex review_response.tex
pdflatex review_response.tex
```

**Note:** The `\printpartbibliography` command from biblatex is no longer supported. All citations will appear in the main bibliography at the end of the document.



### Customization
You can customize the appearance of all the boxes in the `reviewresponse.sty`
file.

**Visual Style (v2.0):**
- Comment boxes feature 3pt rounded corners (`arc=3pt`)
- Soft gradient shadow effect (`drop fuzzy shadow`)
- Enhanced visual hierarchy with professional appearance

If you only want to change the colors of the boxes, you need to redefine the
following colors.
The shown values are the defaults.
```latex
\definecolor{colorcommentfg}{RGB}{0,63,87}  % color of the title in the comment box
\definecolor{colorcommentbg}{HTML}{e0f0f6} % color of the background of the comment box
\definecolor{colorcommentframe}{RGB}{0,112,155} % color of the frame of the comment box

\colorlet{colorchangebg}{black!2} % color of the background of the changes box
\colorlet{colorchangeframe}{black!20} % color of the frame of the changes box
```

**Typography:**
- Paragraph indentation: 2em (English academic standard)
- Paragraph skip: 0.25em
- Uses Fourier font (Utopia family) for elegant appearance
