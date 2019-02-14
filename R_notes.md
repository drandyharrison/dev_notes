% R notes

# Updating R within RStudio, Windows 10

`installr` is the R package which helps install and update software.

The R code you will need for updating R is:

		install.packages("installr")
		library(installr)
		updateR()
	
# Basics

To get the working directory: `getwd()`

To list the files in the current directory: `list.files()`

# Introduction to R

To execute the current line (where the cursor is located) in a script `CTRL+RET`.

# Creating bar charts

Once data are read in, the first task, in any analysis, is to examine the individual variables to check

* the data were entered correctly;
* the data meet the assumptions of the statistical procedures to be used; and
* for any interesting or informative patterns in the data.

For a categorical variable the easiest way to the data is to create a bar chart.

When analysing quantitative data - such as age - the commonest charts to investigate them are hostograms (like bell curves) and box plots. A box plot is way to look at the distribution that highlights outliers. It can give an idea of what might be unusual or exceptional in the distribution.

In a boxplot, the dotted lines (or whiskers) of the box plot go to the highest and lowest non-outlier values. If there are outliers they will be indicated by circles beyond the whiskers of the box plot.