#Data Exploration in Azure Machine Learning Studio

Often times the first thing a data science practitioner does before building any ML models, is to explore the data and formulate intuitions on what can be done with the data. This kind of exploratory data analysis is essential to understand the characteristics of the data before building data models techniques or perform hypothesis testing.

Azure ML provides many ways to facilitate exploratory analysis out of the box. This article offers a quick tour of the common approaches. 

## Data visualization

One of the most popular features in Azure ML is the ability to visualize a dataset right in the experimente graph. Simply point the mouse at any output port, then click (either left-click or right-click; they both work the same way!) on the port, and choose "Visualize" on the output port context menu. You can also rigt-click on the module and the navigate through cascading menu which leads to the "Visualize" menu item of the particular output port. 

![Visualize context menu](http://test.com)

The Data Visualization screen offers a convenient way to quickly understand the data visually. If the select port type is dataset, the below is what you typically whould see.

![Visualize screen](http://test.com)

First of all, notice it shows the navigation breadcrumb that reminds you the name of the experiment, the name of the module and the name of the output port of the dataset that's being visualized currently. On the top right hand corner, it shows the number of rows and columns the current dataset has. It then displays a table containing data from the first 100 columns (starting from the left-most column) and the first 100 rows. Below the column name, it displays a mini histogram. By glancing on the mini histogram, you get a quick idea on the distribution of the data in that column. Numerical columns are automatically discretized into 10 bins to display the histogram. For string or categorical values, the histogram includes counts of the 10 most frequent values.

You can then select a column by clicking on the column header or any row of that column in the data table. On the right hand side, you get some basic statics for the selected column. The first thing you should pay attention to, is the _Feature Type_ field. It displays the data type of the column (numerical, string or categorical), as well as additinal metadata that marks the column a _feature_ column, a _label_ column, or a _weight_ column. This is signficant because many modules, expecially machine learning modules, applies different logic to columns based on this metadata. For example, _Train Model_ module uses the column with _label_ metadata as training target values, it takes all _feature_



## Summarize data


## Compute advanced statistics.

## Use Execute R or Python Script module to select a subset. 

## Use built-in R or Python JuPyteR Notebook  
