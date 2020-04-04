# Personalized Marketing Campaign for Starbucks

(in association with Udacity)

## Project Motivation

Being a constant customer at Starbucks, I found this project interesting. Also, this is a real-life use case (even though with simulated data) this project has been a great oppurtunity to showcase my Data Science skills on one hand and improve my skill-set on the other 😁

## Running the project on local:

- Simply download the jupyter notebook (`SBUX_Personalized_Marketing_Campaign.ipynb`) and the 3 data files.
- [Click here](https://drive.google.com/open?id=1JciCsDrTwwBk6o77aY0hLpf5iLFkUlUF) for data.
- In your terminal run, 
  - `cd directory/to/ipynbfile` 
  - `jupyter notebook`
  - The Jupyter notebook will open in your default browser at `http://localhost:8888/tree`

## I. Understanding the Business

**Starbucks Corporation** is an American **coffee company and coffeehouse chain**. Starbucks locations serve hot and cold drinks, whole-bean coffee, microground instant coffee known as VIA, espresso, caffe latte, full- and loose-leaf teas including Teavana tea products, Evolution Fresh juices, Frappuccino beverages, La Boulange pastries, and snacks including items such as chips and crackers; some offerings (including their annual fall launch of the Pumpkin Spice Latte) are seasonal or specific to the locality of the store. Many stores sell pre-packaged food items, hot and cold sandwiches, and drinkware including mugs and tumblers; select "Starbucks Evenings" locations offer beer, wine, and appetizers. Starbucks-brand coffee, ice cream, and bottled cold coffee drinks are also sold at grocery stores. Source - [Wikipedia](https://en.wikipedia.org/wiki/Starbucks).

### - Introduction 

Once every few days, Starbucks sends out an offer to users of the mobile app. An offer can be merely an advertisement for a drink or an actual offer such as a discount or BOGO (buy one get one free). Some users might not receive any offer during certain weeks. Also, not all users receive the same offer.

### - Goal

- Given data set is a simplified version of the real Starbucks app because the underlying simulator only has one product whereas Starbucks actually sells dozens of products. It contains simulated data that mimics customer behavior on the Starbucks rewards mobile app.
- The **goal** is to combine transaction, demographic and offer data to determine which demographic groups respond best to which offer type.
- So the guiding questions are - 
    1. Do people react to different promotions differently? 
        - If yes, how do people react to different promotions? 
    2. What are the factors affecting these reactions?

## II. Understanding the Data

The data is contained in three files:

* `portfolio.json` - containing offer ids and meta data about each offer (duration, type, etc.)
* `profile.json` - demographic data for each customer
* `transcript.json` - records for transactions, offers received, offers viewed, and offers completed

Here is the schema and explanation of each variable in the files:

**Dataset 1: `portfolio.json`**
* id (string) - offer id
* offer_type (string) - type of offer ie BOGO, discount, informational
* difficulty (int) - minimum required spend to complete an offer
* reward (int) - reward given for completing an offer
* duration (int) - time for offer to be open, in days
* channels (list of strings)

**Dataset 2: `profile.json`**
* age (int) - age of the customer 
* became_member_on (int) - date when customer created an app account
* gender (str) - gender of the customer (note some entries contain 'O' for other rather than M or F)
* id (str) - customer id
* income (float) - customer's income

**Dataset 3: `transcript.json`**
* event (str) - record description (ie transaction, offer received, offer viewed, etc.)
* person (str) - customer id
* time (int) - time in hours since start of test. The data begins at time t=0
* value - (dict of strings) - either an offer id or transaction amount depending on the record


Every offer has a validity period before the offer expires. As an example, a BOGO offer might be valid for only 5 days. It is obeserved that in the data set that informational offers have a validity period even though these ads are merely providing information about a product; for example, if an informational offer has 7 days of validity, one can assume the customer is feeling the influence of the offer for 7 days after receiving the advertisement.

The given transactional data shows user purchases made on the app including the timestamp of purchase and the amount of money spent on a purchase. This transactional data also has a record for each offer that a user receives as well as a record for when a user actually views the offer. There are also records for when a user completes an offer. 

## III. Preparing the Data 

After performing necessary exploratory data analysis and other cleaning tasks (which I have explained in the jupyter notebook as I move forward), I have merged the three dataset into one. Further, I have split this dataset into two parts. 
1. Dataframe consisting of all the data related to Offers (`offers_df`)
2. Dataframe consisting of all the data related to Transactions (`transactions_df`)
I have also performed One Hot Encoding and Label encoding wherever necessary on the `object` dtype variables.

## IV. Data Modelling

### Unsupervised Learning:
KMeans Clustering is applied on the data to find groups of customers and identify the factors affecting reactions of customers to different offers.

### Supervised Learning:
A predictive model is built to predict which offer type a customer is most likely to interact with if we have that customer's past data. K Nearest Neighbours Classification is chosen after training the data on various classifiers because KNN Classifier does not overfit and gives good testing accuracy around `75%`

## Evaluting the Results - Conclusion:

1. From the visualization in unsupervised Learning, it can be inferred that **income does not matter in customers' purchasing habits** because the Total number lies between 0 to 1500 regardless of the customers' income.
2. Compared to BOGO and Discount offer, the **informational offers are not much popular**.
3. **Males** with **income range 30000.0 to 70000.0** tend to **spend more than Females** and Other Genders for the BOGO and Discount Offers
4. **Females** with **income range 71000.0 to 120000.0** tend to **spend more than Males** and Other Genders for the BOGO and Discount Offers.
5. The Offers which are of types **BOGO and Discount** are the most viewed with dollar **rewards 3, 10, 5, 2** respectively.
6. The Offers of type, **Buy One Get One (BOGO) and Discount** are the only offers that **are completed** by the customers.
7. **BOGO** being the most popular Offer Type, it is mostly **used by the Males** followed by the Females.
8. In the late 2017, the number of daily sign-ups had crossed the 500-mark, which was between 200-400, back in 2016. But this number decreased subsequently in 2018.
9. **BOGO** being the most popular Offer Type, it is mostly **used by the ADULT age group** of customers followed by the ELDERLY age group
10. Answers to our guiding questions: 
  - People react to different promotions differently.
  - Customers are attracted to BOGO and Discount offers more as compared to Informational Offers
  - Factors like **Age, Gender, Income** of the *customers* and the **Rewards** which customers receive from each *offer* are the factors which affect the customers reactions positively. 

### Further Improvement:
- Using `transactions_df`, average amount can be calculated. Or a supervised learning model can be built to predict the amount a customer will spend in future on various offers.
- Hyper Parameter Optimization i.e. GridSearchCV can be used to improve the KNN classifier and identify the model parameters.

## Acknowledgments
Thank you to Udacity for such amazing opportunity and lessons. Thank you the Starbucks for sharing this use case and the simulated data. 
Also thanks to the [pandas](https://pandas.pydata.org/), [sklearn](https://scikit-learn.org/stable/index.html) and [seaborn](https://seaborn.pydata.org/) communities for their awesome and lucid official documentations which I have used for reference.

Do check out [my blog](https://medium.com/@ranadesammit/personalised-marketing-campaign-for-starbucks-e01c1e2a11ec) on Medium! 
