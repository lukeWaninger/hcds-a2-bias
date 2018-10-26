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
To create these tables, we will draw from two data sources:
1. Wikipedia Article Data found on [Figshare](https://figshare.com/articles/Untitled_Item/5513449).

| field   | data type | description                    |
|---------|-----------|--------------------------------|
| page    | str       | article title                  |
| country | str       | full country name              |
| rev_id  | int       | revision identification number |

2. Population Data found at a random [DropBox](https://www.dropbox.com/s/5u7sy1xt7g0oi2c/WPDS_2018_data.csv?dl=0) location.


| field                          | data type | description                                 |
|--------------------------------|-----------|---------------------------------------------|
| Geography                      | str       | full country name                           |
| Population mid-2018 (millions) | str       | population in millions recorded in mid-2018 |

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

### The Objective Revision Evaluation Service ([ORES](https://www.mediawiki.org/wiki/ORES)) 
This API will be used to estimate the quality of each article drawn from source 1 above. Data will be gathered from this source through formed API requests in the notebook. ORES will return an estimated article quality and probabilities for six different rankings.
1. FA - Featured article
2. GA - Good article
3. B - B-class article
4. C - C-class article
5. Start - Start-class article
6. Stub - Stub-class article

You may also notice two additional categories not to be confused with the six designated above. They are error results from the ORES API and may be either 'Text Deleted' or 'Revision not Found'.

## Files Created
This notebook creates 1 CSV file of data extracted and compiled as part of this analysis.

| name | datatype | descriptions |
|------|----------|--------------|
| country | str | the country being referenced |
| article name | str | name of Wikipedia article |
| revision_id | int | the revision id referenced for when quering ORES for article quality prediction |
| article_quality | str | the predicted quality of article |
| population | int | population count in millions of people |

### Provenance
_[See the graph](https://www.synapse.org/#!Synapse:syn17015603)_

![Provenance Graph](https://github.com/lukeWaninger/DATA512_A2/blob/master/provenance.png)

## License
This assignment code is released under the MIT license.
Data Source Licenses:
* Figshare - [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)
* DropBox - *None Specified in Document Source*

## Results
I began this project with the notion that bias would be easily identified for a number of reasons. First, each country has a different level of access to internet resources. Second, many countries filter the content for which their population can access. The most pervasive of which is North Korea which is reflected in the dataset. Third, Wikipedia itself will have a different level of presence within each country. And lastly, the education level of a population will vary across countries. This is in no way an inclusive set and only one of which is can be directly related to ethical issues (goverment filtering).  All of these create could potentially be a source of variance amongst the resulting dataset. This being said, bias was found but I was suprised at how drastically the data is skewed. First check out the ten countries with the most articles per million people.

| country                        | articles_per_million |
|--------------------------------|----------------------|
| Tuvalu                         | 5500                 |
| Nauru                          | 5300                 |
| San Marino                     | 2733.3               |
| Monaco                         | 1000                 |
| Liechtenstein                  | 725                  |
| Tonga                          | 630                  |
| Marshall Islands               | 616.7                |
| Iceland                        | 515                  |
| Andorra                        | 425                  |
| Federated States Of Micronesia | 380                  |

And the ten with the least.

| country      | articles_per_million |
|--------------|----------------------|
| Vietnam      | 2                    |
| Bangladesh   | 1.9                  |
| Thailand     | 1.7                  |
| Korea, North | 1.5                  |
| Zambia       | 1.5                  |
| Ethiopia     | 1                    |
| Uzbekistan   | 0.9                  |
| China        | 0.8                  |
| Indonesia    | 0.8                  |
| India        | 0.7                  |

The ten countries with the highest percentage of quality articles.

| country                  | percent_quality |
|--------------------------|-----------------|
| Korea, North             | 0.179           |
| Saudi Arabia             | 0.134           |
| Central African Republic | 0.118           |
| Romania                  | 0.115           |
| Mauritania               | 0.096           |
| Bhutan                   | 0.091           |
| Tuvalu                   | 0.091           |
| Dominica                 | 0.083           |
| United States            | 0.075           |
| Benin                    | 0.074           |

And the least quality.

| country      | percent_quality |
|--------------|-----------------|
| Namibia      | 0.006           |
| Sierra Leone | 0.006           |
| Brazil       | 0.005           |
| Bolivia      | 0.005           |
| Fiji         | 0.005           |
| Morocco      | 0.005           |
| Lithuania    | 0.004           |
| Nigeria      | 0.004           |
| Peru         | 0.003           |
| Tanzania     | 0.002           |

The most suprising thing to me was the quality of articles. We see that North Korea has only 1.5 articles per million people but of those articles, they have high percentage of good quality. I don't know who wrote these articles. Maybe the reason for such a high percentage is because the originating authors are from western sources  or this is a result of North Korean governance. The ten lowest quality do not necessarily suprise me. These are countries are neither English speaking or known to have great public education systems that would lead to high quality articles being written. The tables alone don't give a general perspective of how far outlying some of these data are. I would expect, with no bias, a more symmetric distribution. These, however, are incredibly right skewed. See the static visualization below, or click the interactive plot for hover events.

_[See the interactive plot](https://plot.ly/~waninger/5/)_  
  
![Final Visualization](https://github.com/lukeWaninger/hcds-a2-bias/blob/master/hcds-ad-bias.png)

### Future Work
The analysis in this notebook leads to several more questions in regards to the where this bias comes from. Obviously a strong bias exists. Joining this dataset with the world indicators could bring to light more meaningful insights into the problem.

