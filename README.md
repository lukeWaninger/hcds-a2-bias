# Bias in Data
Name: Luke Waninger

Date: 24 October 2016

## Goal
> The goal of this assignment is to explore the concept of bias through data on Wikipedia articles - specifically, articles on political figures from a variety of countries. 
In the analysis portion of the notebook I will show two major items:
> 1. The countries with the greatest and least coverage of politicians on Wikipedia compared to their population.
> 2. The countries with the highest and lowest proportion of high quality articles about politicians.
[HCDE Fall 2018 - A2](https://wiki.communitydata.cc/Human_Centered_Data_Science_(Fall_2018)/Assignments#A2:_Bias_in_data)

## Data sources used
To create these tables, we will draw from three data sources:
1. Wikipedia Article Data found on [Figshare](https://figshare.com/articles/Untitled_Item/5513449).
2. Population Data found at a random [DropBox](https://www.dropbox.com/s/5u7sy1xt7g0oi2c/WPDS_2018_data.csv?dl=0) location.
3. The Objective Revision Evaluation Service ([ORES](https://www.mediawiki.org/wiki/ORES)) will be used to estimate the quality of each article drawn from source 1 above.

## Resources used
This analysis was prepared using Python 3.7 running in a Conda environment. The environment dependencies can be installed via `pip install -r requirements.txt`.
Documentation for Python can be found here: https://docs.python.org/3.7/  
Documentation for Jupyter Notebook can be found here: http://jupyter-notebook.readthedocs.io/en/latest/  

The following Python packages were used and their documentation can be found at the accompanying links:
* [`io`](https://docs.python.org/3/library/io.html)
* [`itertools`](https://docs.python.org/2/library/itertools.html)
* [`json`](https://docs.python.org/3/library/json.html)
* [`multiprocessing`](https://docs.python.org/2/library/multiprocessing.html)
* [`requests`](http://docs.python-requests.org/en/master/)
* [`IPython`](https://ipython.org/documentation.html)
* [`numpy`](https://docs.scipy.org/doc/)
* [`pandas`](https://pandas.pydata.org/)
* [`plotly`](https://plot.ly/python/)
* [`synapse`](https://python-docs.synapse.org//)
* [`zipfile`](https://docs.python.org/2/library/zipfile.html)

## Files Created
This notebook creates 1 CSV file of data extracted and compiled as part of this analysis.

### Provenance
_[See the graph](https://www.synapse.org/#!Synapse:syn17015603)_

![Provenance Graph](https://github.com/lukeWaninger/DATA512_A2/blob/master/provenance.png)

| name | datatype | descriptions |
|------|----------|--------------|
| country | str | the country being referenced |
| article name | str | name of Wikipedia article |
| revision_id | int | the revision id referenced for when quering ORES for article quality prediction |
| article_quality | str | the predicted quality of article |
| population | int | population count in millions of people |

Notes on article quality. This is an ordinal variable with six possible rankings.
1. FA - Featured article
2. GA - Good article
3. B - B-class article
4. C - C-class article
5. Start - Start-class article
6. Stub - Stub-class article
You may also notice two additional categories not to be confused with the six designated above. They are error results from the ORES API and may be either 'Text Deleted' or 'Revision not Found'.

## License
This assignment code is released under the MIT license.
Data Source Licenses:
* Figshare - [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)
* DropBox - *None Specified in Document Source*

## Results
I began this project with the notion that bias would be easily identified for a number of reasons. First, each country has a different level of access to internet resources. Second, many countries filter the content for which their population can access. The most pervasive of which is North Korea which is reflected in the dataset. Third, Wikipedia itself will have a different level of presence within each country. And lastly, the education level of a population will vary across countries. This is in no way an inclusive set and only one of which is can be directly related to ethical issues (goverment filtering).  All of these create could potentially be a source of variance amongst the resulting dataset. This being said, bias was found but I was suprised at how drastically the data is skewed. I would expect, with no bias, a more symmetric distribution. These, however, are incredibly right skewed. See the static visualization below, or click the interactive plot for hover events.

_[See the interactive plot](https://plot.ly/~waninger/5/)_
![Final Visualization](https://github.com/lukeWaninger/hcds-a2-bias/blob/master/hcds-ad-bias.png)

