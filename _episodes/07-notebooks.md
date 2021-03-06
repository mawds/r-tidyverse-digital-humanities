---
title: "Combining your code with text"
teaching: 20
exercises: 10
questions:
- "How can I organise my work using Rmarkdown documents?"
objectives:
- "To understand the RMarkdown syntax"
- "To understand how to create and use a markdown document"
- "To understand how to use Knitr to write reports"

keypoints:
- "Notebooks let us combine R code and text explaining our analysis"
source: Rmd
---



## Introduction

So far today we've written scripts to load, analyse and plot data.   We've also discussed how to save data and plots.  It can often be useful to combine our analysis and a written explanation of what we've done.    This is different from commenting our code (which we should be doing anyway); instead we're talking about writing up our analysis while doing it.

> ## Jupyter / Python notebooks 
> This is a similar idea to a [Jupyter notebook](http://jupyter.org/), but is integrated within R Studio.
{:.callout}

Let's get started by making a new notebook.  From the `File` menu, choose `New file` and then `Rnotebook`.   A new window will open containing an example notebook:

![example notebook figure](../fig/99-notebook.png)

The notebook includes "chunks" of text, and chunks of R code.

The start of an R code region is marked with &#96; &#96; &#96; &#123; &#114; &#125; The end of an code region is marked with &#96; &#96; &#96;  These are a little awkward to type; pressing <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> will insert a new chunk of R code into your document.  You can (and should) label your chunks of R code:

 &#96; &#96; &#96; &#123; &#114; mychunk &#125; 

This makes it easier to jump between chunks within your document, using the selector box a the lower left of the edit window.

The header at the start of the notebook (between the `---`s) contains metadata which tells R how to process the notebook.  This can be edited by hand (for example to change the "title:" field), or to add an "author: " field.  R Studio may also modify it, for example, if you change the output format of the document.

Before we go any further, make a new subdirectory for your notebooks, for example, `notebooks`. and save the notebook in it using `File`, `Save`.  We need to do this so that we can preview and build the notebook.   When you run code in your notebook, RStudio will set the working directory to be the notebook's directory.  This means that if we want to load some data from our `data` folder, we will need to use the path `../data/twitterData.csv` (rather than `data/twitterData.csv`, as we used previously).  The `..` tells R to look in the parent directory of the working directory.  

## Running notebooks

We can run the notebook interactively within R Studio.  Press the "Run" button (at the top of the editor window) and choose "Run all" (or press <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>R</kbd>).   This will execute each chunk of code within R Studio and show us the results of each chunk within the document. This makes it easier to interactively edit our code, look at the results of our analysis, and edit our text within the same environment.

We can preview the notebook by selecting "Preview notebook" from the top of the editor window.  This will render the text and code into an html document.   Note that the preview will use executed chunks of R code in the editor window.  For this reason it is a good idea to choose "Restart R and run all chunks" from the run button (at the top of the editor).  This will ensure your code has been run in order, and that it is self consistent.

## Example

As an example of using notebooks, let's use the Twitter data, and some of the ideas introduced earlier to run, and to document, an analysis of the data.  I'll do this as a running demonstration, to illustrate the principles.    

As these lessons are written in R Markdown, it is difficult to show the markdown itself within them.  For this reason, you will need to click the links where indicated.  This will show you the contents of the Markdown document; copy the entire contents of the webpage into a new R notebook (overwriting the example notebook), and save it in `notebooks` directory you made in your project directory.   Make sure it has the extension `.Rmd`; this way RStudio will know it is a notebook and handle it appropriately.



We can modify the example notebook to load the twitter data into our working environment, and to print of extract of it.  The notebook to do this can be found [here](https://raw.githubusercontent.com/UoMResearchIT/r-tidyverse-digital-humanities/gh-pages/notebooks/example1.Rmd)

## Controlling what's output

At the moment all the code and data we've written are shown in the document.  This can be excessive.  For example, we may get diagnostic messages which we don't anticipate being of interest to the reader.  We can hide the R code in a chunk as follows: 

 &#96; &#96; &#96; &#123; &#114; mychunk echo=FALSE &#125; 

We can hide messages printed to the screen with:

 &#96; &#96; &#96; &#123; &#114; mychunk message=FALSE &#125; 

Note that we can exclude all of the output of a chunk with:

 &#96; &#96; &#96; &#123; &#114; mychunk include=FALSE &#125; 

You may need to do this to suppress package start-up messages; these are handled by R in a slightly different way from regular messages.
 
Options can be combined by separating them with commas:

 &#96; &#96; &#96; &#123; &#114; mychunk echo=FALSE, messages=FALSE &#125; 
 
> ## Other options
> 
> Warnings and errors can be suppressed with "warning=FALSE" and "error=FALSE".  You should use these options with care; warnings and errors usually happen for a reason!.  "eval=FALSE" will include the chunk (i.e. you'll see the R code, provided "echo=TRUE"), but it won't evaluate it.  This can be useful when you want to avoid running a slow piece of your analysis, for example.
{: .callout}

You can set the default options for all subsequent chunks by including, e.g., in an R code chunk:


~~~
knitr::opts_chunk$set(echo = FALSE, warning = TRUE)
~~~
{: .language-r}

You would typically include this in your setup chunk, and use `include=FALSE` so as not to output the code or output of the setup chunk itself.

How much of the "behind the scenes" work you show in a notebook is up to you, and will depend on the intended audience.   If you hide all the code, you can produce something which looks very much like a regular scientific paper.  The benefit of writing a paper like this is that your analysis and write up are in the same place.   If your analysis (or data) change, the paper will be updated automatically.   By keeping the underlying R Markdown file it is possible for you, or others to work out exactly how each figure in you work was produced.

[This example](https://raw.githubusercontent.com/UoMResearchIT/r-tidyverse-digital-humanities/gh-pages/notebooks/example2.Rmd) shows the effect of using `include=FALSE` and `echo=FALSE` to hide the package loading messages and our R code.

We can also display R output "inline" (i.e. so it appears as normal text within a paragraph):  For example:
<pre>
The sine of 0 is &#96;r sin(0)&#96;
</pre>

Will display as:

The sine of 0 is 0

## Formatting our text

We can format our notebook using _markdown_.  For example, to make some text italic, we use:

<pre>
_This text is italic._ This text isn't
</pre>
Which will appear as:

_This text is italic._ This text isn't

R Studio has a quick reference guide to common markdown formatting codes. This can be found under "Help", "Markdown quick reference".  There is also a more comprehensive cheat sheet under the help menu, and an even more comprehensive reference guide.

[LaTeX equations](https://en.wikibooks.org/wiki/LaTeX/Mathematics) can be included in your notebook as follows:

<pre>
$$a=\pi r^2$$
</pre>

Which will appear as:

$$a=\pi r^2$$

You can insert an equation within a line of text by enclosing the LaTeX code within single dollars.

> ## More complicated formatting
> 
> It is also possible to combine R code and LaTeX text.  This approach is better suited to producing a "static" document, such as a paper, rather than a notebook.  To do this, choose "File", "New", "R Sweave".   R Studio will produce a skeleton document. As with notebooks, <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>I</kbd> will insert a new R code chunk.  To display inline R code use:
> <pre>
> The cos of 0 is \Sexpr{cos(0)}
> </pre>
> which will display as "The cos of 0 is 1".
{: .callout}

##  Doing more with Markdown and notebooks

We sometimes want to include the output of of statistical analysis (such as the results of the models we
fitted using `lm()`.  The [`pander`](https://cran.r-project.org/web/packages/pander/index.html) package 
will add the appropriate markdown formatting to many R functions to make them display nicely.  Having installed
and loaded the `pander` package,  run the `pander()` function on the object you wish to display, e.g.


~~~
library("pander")
pander(uk_lifeExp_model_squared)
~~~
{: .language-r}

Make sure you use the option `results='asis'` on the code chunk; this will allow the markdown formatting generated by `pander` to be processed. 


In this episode we've looked at how to make notebooks, and how to compile these into Word, PDF and HTML files.
[The British Ecological Society has published](https://www.britishecologicalsociety.org/wp-content/uploads/2017/12/guide-to-reproducible-code.pdf) an excellent guide on producing reproducible reports using RMarkdown, and on reproducible research more generally (although aimed at Ecologists the approaches they advocate are general).  

The book [Reproducible Research with R and RStudio, by Christopher Gandrud](https://www.librarysearch.manchester.ac.uk/primo-explore/fulldisplay?docid=44MAN_ALMA_DS21275136220001631&context=L&vid=MU_NUI&search_scope=BLENDED&tab=local&lang=en_US) also explains this approach.


We can use a similar approach to produce other types of outputs. The [RMarkdown gallery](http://rmarkdown.rstudio.com/gallery.html) contains examples of the many different types of document you can produce (some of these may require a newer version of R Studio than the one installed on the PC clusters).

This course was written in R Studio.  The slides I used to introduce the course at the start were written as an R Markdown document and each episode of this course is written as an R Markdown document (although the conversion to an HTML page is a little more complex than for the examples we looked at - this is so that the formatting of the challenges etc. works properly).   You can see all of the underlying R Markdown for this course on [Github](https://github.com/uomresearchit/r-tidyverse-intro/), in the `_episodes_rmd` directory; having selected an episode you will need to click the "raw" button to see the markdown itself.  



