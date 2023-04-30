DESCRIPTION
----------
This package describes our website visualization application. The visualization summarizes the results of our textual analysis of over 10 million lodging reviews, shown in three distinct maps. Each map focuses on one aspect of the analysis, and results are aggregated by location (city/county) and quarter of the year. The aggregation includes 21 locations and 13 quarters to allow visualization over both time and space. The visualization is contained on one webpage and each has an interactive element.


The first map displays consumer sentiment of lodging reviews in terms of positive, negative, and neutral reviews. The sentiment was calculated using VADER, a textual analysis algorithm that generates a compound polarity score for each review. Compound scores of zero are classified as a neutral review, while positive and negative compound scores are assigned their respective labels. The second map displays the quantity of reviews collected by location and quarter. A bubble data element is sized according to the quantity of reviews, and a user can determine the changes over time with an interactive slider-bar. The third map displays the top five words from the top five topics within reviews in the form of a word cloud. These topics and key words were calculated using LDA, a textual analysis algorithm employing a Bayesian mixture model to derive topics and their component words.


Additionally, we have included the Python notebooks used to clean the data and generate the NLP models, should the user wish to replicate the process used to create the webapp datasets.


INSTALLATION
----------
The web application requires the user to have a simple local web-server (e.g. python3) and a web browser installed. The web application was created using Google Chrome version 88, which is the preferred browser for viewing the web application.  Firefox version 87 was also tested, but some textual issues were present, where words did not have their proper font sizes in the word cloud.


If the user wishes to perform the data cleaning and model generation processes, then they would also need to have the appropriate libraries to do so. Installing the python3 anaconda distribution would be recommended in this case https://www.anaconda.com/products/individual. The user would also need to install the gensim library https://radimrehurek.com/gensim/. Additional python packages (e.g., numpy, pandas) are imported in the notebook scripts directly.


EXECUTION
----------
The following is a link to a demo video that can guide the user on how to launch the web application: https://youtu.be/xnCFQIE_6cQ


Start a simple web-server from the root directory of the web_app folder.  One way of doing this is with python3.  For example, in the web_app folder from a Linux command prompt, type ‘python3 -m http.server’ without the quotes.  The web application should successfully start. Enter http://localhost:8000/  in the url bar of a Google Chrome browser (port may be different depending on the web-server being used). You should be able to see the web application in the browser window.


Once the webpage is loaded from the server, the three maps are displayed in a portrait layout, one above the next. Scroll along the right-hand side of the page to change the display to a different map. Each map includes instructions at the bottom, a slider-bar to select a time-quarter, and a tool-tip for additional information for every location. 


If a user would like to perform the data cleaning and model generation processes, then they should begin with the data collection process. Airbnb data is located at http://insideairbnb.com/get-the-data.html, where the user can download the listings.csv.gz and reviews.csv.gz files for January of 2018-2021 for each American location. They would also need to create an Apify account, and use the following web scraping tool to collect the Tripadvisor reviews for the same American locations in the Airbnb dataset:  https://apify.com/maxcopell/tripadvisor.


The user would then need to clean the data using the ‘Airbnb data prep one city.ipynb’ notebook on the Airbnb files, and the ‘Data Cleaning TripAdvisor.ipynb’ notebook on the TripAdvisor files.


Once the files are cleaned then the user can start the model generation process. The user should create a central data folder where all of the cleaned Airbnb and TripAdvisor files are stored. The user may then run the ‘ApplyVADERModel.ipynb’ notebook, which will combine all of the files, filter out non-English reviews, and give the sentiment scores for each review. The user will next be able to run the ‘ApplyLDAModel.ipynb’ notebook, which will train the LDA model, and yield the best topic for each review. The user may run ‘VADER output labeling and sampling.ipynb’ and ‘ApplyTopicCoherence.ipynb’ to validate the sentiments and topics generated, respectively.


Finally, the user can run the ‘Data aggregation for visualization.ipynb’ notebook which will aggregate the output generated from the model notebooks. These aggregated files will allow for quicker visualization generation and minimize the storage footprint for production servers.


FILES INCLUDED
----------
* Web Application
   * CODE/web_app/index.html
   * CODE/web_app/data/ldaCityQ.csv
   * CODE/web_app/data/ldaTopics.csv
   * CODE/web_app/data/us-cities.csv
   * CODE/web_app/data/us-states.json
   * CODE/web_app/data/vaderCityQ.csv
   * CODE/web_app/lib/d3-legend.min.js
   * CODE/web_app/lib/d3-tip.min.js
   * CODE/web_app/lib/d3.layout.cloud.js
   * CODE/web_app/lib/d3.v5.min.js
* Cleaning Scripts
   * CODE/VADER output labeling and sampling.ipynb
   * CODE/Data Cleaning TripAdvisor.ipynb
   * CODE/Data aggregation for visualization.ipynb
   * CODE/Airbnb data prep one city.ipynb
* NLP Scripts
   * CODE/ApplyLDAModel.ipynb
   * CODE/ApplyVADERModel.ipynb
   * CODE/ApplyTopicCoherence.ipynb
* Documentation
   * DOC/team085poster.pdf
   * DOC/team085report.pdf
   * ReadMe.txt