### "[The Consumption Response to Trade Shocks: Evidence from the US-China Trade War](http://www.waugheconomics.com/uploads/2/2/5/6/22563786/waugh_consumption.pdf)"

![](simple_county_by_quantile.png)

This repository contains code to reproduce aspects of the paper ["The Consumption Response to Trade Shocks: Evidence from the US-China Trade War."](http://www.waugheconomics.com/uploads/2/2/5/6/22563786/waugh_consumption.pdf) Only results associated with non-proprietary data are available, i.e. Chinese retaliatory tariffs and it's projection to the county level and then their correlation with trade and employment. The auto analysis notebook is **not** included here as the data used is proprietary.

---

**Update (12/2019)** The paper and aspects of the code have been revised relative to the September 2019 [NBER working paper](https://www.nber.org/papers/w26353) version. Below are some key updates:

- An alternative concordance is used. To reproduce the NBER version results, read the notes around code cell 15 in [``countylevel_tariffs_and_exports.ipynb``](https://github.com/mwaugh0328/consumption_and_tradewar/blob/master/countylevel_tariffs_and_exports.ipynb) and uncomment the appropriate parts.

- I now use the BLS single files rather than the county high-level files. I will keep the [``bls_quarterly_county.ipynb``](https://github.com/mwaugh0328/consumption_and_tradewar/blob/master/bls_quarterly_county.ipynb) file in the repository, but now to generate the files you must use [``bls_single_file.ipynb``](https://github.com/mwaugh0328/consumption_and_tradewar/blob/master/bls_single_file.ipynb). The BLS data now goes to June 2019. In this notebook, I also layer in population, income, rural share data from the Census.

- Pretrends. The notebook [``pretrend_notebook.ipynb``](https://github.com/mwaugh0328/consumption_and_tradewar/blob/master/pretrend_notebook.ipynb) now provides an exploration of pretrend issues in employment data. This notebook essentially mimics what is done for autos.

- In the paper and the notebooks, population is now used as the main weighting variable rather than employment. To revert to the previous results, simply change the weighting variable to ``total_employment``.

- A driver file that runs everything and reports results discussed in the paper is posted as [``main_driver_file.ipynb``](https://github.com/mwaugh0328/consumption_and_tradewar/blob/master/main_driver_file.ipynb). Also you can use this file to inspect the output, etc.

---

There are several files associated with this repository. Almost all of the notebooks directly pull data from the original source (trade data using the [Census International Trade API](https://www.census.gov/data/developers/data-sets/international-trade.html), concordance from the US Census, employment data from the [BLS](https://www.bls.gov/cew/downloadable-data-files.htm), [shapefiles from the US Census](https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.2017.html)). After running the files, most of the output is saved as a  ``.parquet`` files and stored in the data folder.

Below is a description of each jupyter notebook in the repository. If you don't know what a "jupyter notebook" is or what to do with them, this website is a great place to start: [https://datascience.quantecon.org/](https://datascience.quantecon.org/).

- [``main_driver_file.ipynb``](https://github.com/mwaugh0328/consumption_and_tradewar/blob/master/main_driver_file.ipynb) Does everything start to finish.

The files below are the individual components and are organized in the sequence for which they must be run if you do not have the intermediate files.

- [``updated_tariff_data.ipynb``](https://github.com/mwaugh0328/consumption_and_tradewar/blob/master/updated_tariff_data.ipynb) which uses and shapes the tariff data from [Bown, Jung, and Zhang](https://www.piie.com/blogs/trade-and-investment-policy-watch/trump-has-gotten-china-lower-its-tariffs-just-toward). I'm hosting their datafile as I had problems with a direct link.

- [``alt_hs_naics_mapping.ipynb``](https://github.com/mwaugh0328/consumption_and_tradewar/blob/master/alt_hs_naics_mapping.ipynb) starts from the Census concordance which provides a mapping from hs10 to naics codes and then creates a mapping from hs6 to naics. In the ``data`` folder there is ``alt_concordance.parquet`` which you can download and directly run to proceed to the next step below.

- [``countylevel_tariffs_and_exports.ipynb``](https://github.com/mwaugh0328/consumption_and_tradewar/blob/master/countylevel_tariffs_and_exports.ipynb) takes the tariff data above and then projects down to the county level, in addition to merging it with US export data and US employment data (just for the year 2017). The projection method simply takes a employment weighted averages of tariffs at the NAICS 3 digit level. Waugh (2019) explains more in detail, in addition to the text in the notebook.

- [``tariff_map.ipynb``](https://github.com/mwaugh0328/consumption_and_tradewar/blob/master/tariff_map.ipynb) using the tariff data above, it creates a map of tariff exposure. It downloads the required shapefiles and then plots the change in a county's tariff at the county level. It assumes that you have a folder below the repository called ``shapefiles`` and then ``county`` and ``state`` for which the code will download and unzip the shapefiles into that folder.

- [``bls_single_file.ipynb``](https://github.com/mwaugh0328/consumption_and_tradewar/blob/master/bls_single_file.ipynb) grabs the [Quarterly Census of Employment and Wages](https://www.bls.gov/cew/) quarterly, single files from the BLS and then creates employment measures at the county-level, monthly frequency. It is then merged with the trade data from above. **Note** the single files are very large and take time to download and unzip. This notebook constructs several measures of employment, total, goods producing, retail employment, non-goods producing. The advantage of the single files is that many different measures of employment can be constructed.  

- [``employment_analysis.ipynb``](https://github.com/mwaugh0328/consumption_and_tradewar/blob/master/employment_analysis.ipynb) performs the employment analysis in Section 5 and has the unweighted regression results as well. The analysis also mimics most aspects of the auto analysis in the paper (e.g., visualizations, tabular analysis, regression results).

- [``pretrend_notebook.ipynb``](https://github.com/mwaugh0328/consumption_and_tradewar/blob/master/pretrend_notebook.ipynb) performs the pretrend analysis, Section 6, and generates figures 5 in paper. Here you must specify the employment measure ``emp_all`` is total employment, ``emp_gds`` is goods employment, ``emp_rtl`` is retail employment.

- [``trade_analysis.ipynb``](https://github.com/mwaugh0328/consumption_and_tradewar/blob/master/trade_analysis.ipynb) performs the trade analysis in Section 5 (us exports to china, exports in total) and it contains the unweighted regression results as well. This notebook [``trade_elasticity.ipynb``](https://github.com/mwaugh0328/measuring-trade-elasticities/blob/master/data-code/trade_elasticity.ipynb) estimates a trade elasticity from the product-level trade data...it's 4!

Finally, I must highlight that there is a [license](https://github.com/mwaugh0328/consumption_and_tradewar/blob/master/LICENSE) regarding this work, it's use, and so forth.

##### Old files

- [``bls_quarterly_county.ipynb``](https://github.com/mwaugh0328/consumption_and_tradewar/blob/master/bls_quarterly_county.ipynb) grabs the [Quarterly Census of Employment and Wages](https://www.bls.gov/cew/) files from the BLS and then creates employment measures at the county-level, monthly frequency. It is then merged with the trade data from above. **Note** there is a place where, depending on if commented, creates a dataset with goods producing employment or total private employment.

##### Other Stuff

- [``political_aspects_of_retaliation.ipynb``](https://github.com/mwaugh0328/consumption_and_tradewar/blob/master/political_aspects_of_retaliation.ipynb) Explores the issue about where the tariffs were directed and how that correlates with the propensity of a county to vote for President Trump. Short answer is yes, but most the variation is about places that export the most to china. The interesting observation is that there is a strong correlation between those that exported a lot to china and the propensity to vote for President Trump.
