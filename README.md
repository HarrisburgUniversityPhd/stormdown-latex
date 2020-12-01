# Table of Contents

   * [stormdown](#stormdown)
      * [Tutorials and examples](#tutorials-and-examples)
      * [Examples of dissertation written with stormdown](#examples-of-dissertation-written-with-stormdown)
      * [How to cite](#how-to-cite)
   * [Requirements](#requirements)
   * [Example output](#example-output)
   * [Usage](#usage)
      * [Compiling your dissertation](#compiling-your-dissertation)
         * [PDF output](#pdf-output)
         * [Gitbook output](#gitbook-output)
         * [Word output](#word-output)
      * [Writing your dissertation](#writing-your-dissertation)
      * [Knitting individual chapters](#knitting-individual-chapters)
      * [Cleaning up generated auxiliary files](#cleaning-up-generated-auxiliary-files)
   * [Customisations and extensions](#customisations-and-extensions)
   * [Limitations](#limitations)
      * [Gotchas](#gotchas)
      * [Output formats](#output-formats)

# stormdown

A Harrisburg University Dissertation Template for R Markdown

## Tutorials and examples

The below videos were originally developed by [@ulyngs](https://github.com/ulyngs) as part of [oxforddown](https://github.com/ulyngs/oxforddown), but the content should still apply.

* [Part 1: Building the entire thesis](https://www.youtube.com/watch?v=Yf1W1BBS9cU)
* [Part 2: Building a single chapter](https://www.youtube.com/watch?v=-EJfCA3VA-I)
* [Part 3: Understanding the file structure](https://www.youtube.com/watch?v=jafgJobOgpc)
* [Part 4: A walk-through example of creating your thesis](https://www.youtube.com/watch?v=uWpinaVSZ6Q)
* [Part 5: The content included in index.Rmd (or: why the introduction chapter is special)](https://www.youtube.com/watch?v=FPlwCj5ZH8M)
* [Part 6: Adjusting the order of chapters](https://www.youtube.com/watch?v=-0M3TuDnu7Y)
* [Part 7: _bookdown.yml: Adjusting build settings](https://www.youtube.com/watch?v=jXYfC8RXTvg)
* [Part 8: Makefile: Adjusting build settings](https://www.youtube.com/watch?v=L6mV8z32RfE)
* [Part 9: The LaTeX templates](https://www.youtube.com/watch?v=o2fd_O1On7g)

For how to write your content with the R Markdown syntax, read through the sample content.

The template uses the [bookdown](https://bookdown.org) R package together with the [HU LaTeX template](https://github.com/HarrisburgUniversityPhd/stormdown/tree/master/templates) originally developed by Maria Vaida, plus lots of inspiration from [stormdown](https://github.com/ismayc/thesisdown), [pagedown](https://github.com/rstudio/pagedown), and especially [oxforddown](https://github.com/ulyngs/oxforddown).

## Examples of dissertations written with `stormdown`

_NOTE_: If you've used this template to write your dissertation, drop either [@markanewman](https://github.com/markanewman) or [@sagarkora](https://github.com/sagarkora) and we will add a link showcasing it!

## How to cite

```bibtex
@misc{stormdown2020,
  author = {Mark Newman and Sagar Kora Venu},
  title = {stormdown: A Harrisburg University Dissertation Template for R Markdown},
  year = {2020},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/HarrisburgUniversityPhd/stormdown}}
}
```

# Requirements

* LaTeX - install the TinyTeX distribution `install.packages("tinytex")`
* [R](https://cran.rstudio.com) and [RStudio version 1.2 or higher](https://www.rstudio.com/products/rstudio/download/#download)
* The R packages `bookdown`, `tidyverse`, and `reticulate` (the other packages you need should be automatically installed when you build this project for the first time in RStudio)

# Example output

* PDF output: see [**docs/_main.pdf**](https://github.com/HarrisburgUniversityPhd/stormdown/blob/master/docs/_main.pdf)
* Gitbook output: see [HarrisburgUniversityPhd.github.io/stormdown/](https://HarrisburgUniversityPhd.github.io/stormdown/)

# Usage

* download the **HarrisburgUniversityPhd/stormdown** repo as a zip.
  (optionally fork the repo, then get it from there
* double-click on **index.Rmd** from file explorer

## Compiling your dissertation

### PDF output

* make sure the first `output` argument is `bookdown::pdf_book`
* click the `Knit` button
* the compiled PDF is saved as **docs/_main.pdf**, and the PDF is opened

![](figures/screenshots/build_all.png)
![](figures/screenshots/compiled_pdf.png)

### Gitbook output

* make sure the first `output` argument is `bookdown::gitbook`
* click the `Knit` button
* the compiled gitbook are stored in the **docs/** folder, and the front page (docs/introduction.html) is opened in a browser

![](figures/screenshots/build_gitbook.png)
![](figures/screenshots/compiled_gitbook.png)

### Word output

* make sure the first `output` argument is `bookdown::word_document2`
* click the `Knit` button
* the compiled MS Word document is saved as **docs/_main.docx** and opened

The Word output has no template behind it, and many things do not work (e.g. image rotation, highlighting corrections).
There are no current plans to update this functionality.

## Writing your dissertation

To use this template to write your dissertation, do the following:

* update the YAML header (the stuff at the top between '---') in **index.Rmd** with your name, college, etc.
* write the individual chapters as **.Rmd** files in the root folder.
* write the front matter (abstract, acknowledgements, abbreviations) and back matter (appendices) by adjusting the **.Rmd** files in the **front-and-back-matter/** folder
* for abbreviations, change **front-and-back-matter/abbreviations.tex** to fit your needs (follow the LaTeX syntax in there)

**.Rmd** files you don't want included in the body text must be given file names that begin with an underscore (e.g. **front-and-back-matter/_abstract.Rmd** and **front-and-back-matter/_acknowledgements.Rmd**).
(Alternatively, specify manually in **_bookdown.yml** which files should be merged into the body text.)

## Knitting individual chapters

To knit an individual chapter without compiling the entire dissertation:
1. open the **.Rmd** file of a chapter
2. add a YAML header specifying the output format(s) (e.g. `bookdown::word_document2` for a word document you might want to upload to Google Docs for feedback from collaborators)
3. Click the `knit` button (the output file is then saved in the root folder)

As shown in the sample chapters' YAML headers, to output a single chapter to PDF, use:

```yaml
output:
  bookdown::pdf_document2:
    template: templates/brief_template.tex
```
This will format the chapter in the HU LaTeX style but without including the front matter (table of contents, abstract, etc)

## Cleaning up generated auxiliary files

By default, when you build the entire dissertation, the auxillary files will be removed (to adjust how this is done, edit **Makefile**).

To clean up files generated when knitting individual chapters, type 'make clean-knits' in the terminal.

# Customisations and extensions

* for some of the common things you might want to do in your dissertation, read through the sample content
* for example, the newly added ['Customisations and extensions' chapter](https://HarrisburgUniversityPhd.github.io/stormdown/customisations-and-extensions.html) (thanks [@bmvandoren](https://github.com/bmvandoren)!) adds tips on how to include PDF pages from a published typeset article in your dissertation, and more!

# Limitations

## Gotchas

* don't use underscores (_) in your YAML front matter or code chunk labels! (underscores have special meaning in LaTeX, so therefore you are likely to get an error, cf. https://yihui.org/en/2018/03/space-pain/)
  * bad YAML: `bibliography: bib_final.bib`
  * good YAML: `bibliography: bib-final.bib`
  * bad chunk label: `{r my_plot}`
  * good chunk label: `{r my-plot}`
* if you want to deploy the gitbook via GitHub pages, then the `/docs` folder must contain a file called **.nojekyll**

## Output formats

* at the moment only PDF and HTML output have been properly implemented

Enjoy!
