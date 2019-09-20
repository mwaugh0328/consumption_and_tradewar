### "The Consumption Response to Trade Shocks: Evidence from the US-China Trade War"

This repository contains code to reproduce aspects of the paper "The Consumption Response to Trade Shocks: Evidence from the US-China Trade War." Only results associated with non-proprietary data are available, i.e. Chinese retaliatory tariffs and it's projection to the county level, trade, and employment results.

There are several files associated with this repository. Almost all of the notebooks directly pull data from there original source (trade data using the Census API, employment data from the BLS). After running the files, most of the output is saved as a  ``.parquet`` files are stored in the data folder.

Below is a description of each individual file. The are organized in the sequence for which they must be run if you do not have the intermediate files.

- [``updated_tariff_data.ipynb``](https://github.com/mwaugh0328/consumption_and_tradewar/blob/master/updated_tariff_data.ipynb) which uses and shapes the tariff data from [Bown, Jung, and Zhang](https://www.piie.com/blogs/trade-and-investment-policy-watch/trump-has-gotten-china-lower-its-tariffs-just-toward).

- [``countylevel_tariffs_and_exports.ipynb``](https://github.com/mwaugh0328/consumption_and_tradewar/blob/master/countylevel_tariffs_and_exports.ipynb) takes the tariff data above and then projects down to the county level, in addition to merging it with US export data and US employment data (just for the year 2017). The projection method simply takes a employment weighted averages of tariffs at the NAICS 3 digit level. Waugh (2019) explains more in detail, in addition to the text in the notebook.

 - [``tariff_map.ipynb``](https://github.com/mwaugh0328/consumption_and_tradewar/blob/master/tariff_map.ipynb) using the tariff data above, it creates a map of tariff exposure. It downloads the required shapefiles and then plots the change in a county's tariff at the county level.
