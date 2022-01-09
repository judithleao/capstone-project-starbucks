# README

## Background: This is the final project for the Udacity Data Science Nanodegree.

## Libraries needed:
* pandas
* os
* numpy
* seaborn
* math
* json
* matplotlib
* pylab
* itertools
* statsmodels
* scipy
* sklearn

## Problem space:

Starbucks carried out an experiment to test the effect of different offers that are sent out to Starbucks app users. The experiment ran for 30 days. Offers can be classified into three *types*:
* BOGO (Buy one get one free)
* Discount
* Informational (no monetary advantage)
In total, 10 different offers were tested.

There are 4 *attributes* an offer type can have:
* reward: (numeric) money awarded for the amount spent [not for type Informational]
* channels: (list) web, email, mobile, social
* difficulty: (numeric) money required to be spent to receive reward [not for type Informational]
* duration: (numeric) time for offer to be open, in days

If Starbucks wants to send out offers in the future, it is relevant for them to know which offers are worth sending and to whom. I am assessing which offers are the most successful based on two success metrics (incremental spend and offer completion), and build a model that predicts offer completion based on demographic and derived variables.

## Business questions

The analysis needs to answer the following sets of questions:

**Stage 1: Relevance of offers**
* Q1.1: Are the different offer types successful?
* Q1.2: Does simply knowing about an offer already lead to higher incremental spend even without offer completion?
* Q1.3: Are there differences in success of different offer types?
* Q1.4: Do certain offer attributes influence the success?

If certain offers are successful, they should be included in Step 2:

**Stage 2: Targeting**
* Q2.1: Based on demographic information, which customer is how likely to react to a certain offer?

## Notebooks:
There are two notebooks which have to be run in the order Starbucks-Wrangling and then Starbucks-Analysis.

## Data:
Three datasets are provided with this repo:
* portfolio, which provides information on the offers
* profile, which provides information on the customers (e.g. demographics)
* transcript, which provides information on events (transact, receive offer, view offer, complete offer)
All three datasets need to be combined to answer the key questions.
Two more datasets are created when the Starbucks-Wrangling notebook is run.
The datasets were provided through the Udacity course and come from Starbucks.

## Blog entry: A blog entry which discusses the most important findings can be found here:  

## Population/Records
The data frame that is used for analysis contains one record per person and offer received for offers that the person was aware of. A consumer can only consciously reject or accept an offer if s/he is aware of it. Therefore, the analysis only includes cases where the customer was aware of the offer. This approach allows Starbucks to understand the true appeal of the offer through offer completion. It also shows them the revenue they can generate from an offer if they make people aware of it.

## Success Metrics
The following metrics will be used as measures of success or as dependent variables in the various analyses:

* **Incremental spend**: Type continuous. Money spent over and above what a person would have spent if s/he hadn't been aware of the offer.

* **Offer completion**: Type binary. Not for informational offer. This variable is coded 0 for "viewed, but not used" and 1 for "viewed and used".

## Data Wrangling:
The transcript data requires elaborate pre-processing. This is due to the fact that one consumer can have multiple active offers at the same time. These offers can in fact be the same offer. Data wrangling identifies which view and complete events belong to which received offer event, and which transactions should be allocated to which offer.
The result of the pre-processing is the data frame that gets used for analysis in the notebook Starbucks-Analysis.

## File data-wrangling-overview:
A graphic representation of the different data pre-processing steps. It matches the sections in the Starbucks-Wrangling notebook.

## Analysis:
Various assumptions need to be made prior to analysing the data:
*Assumption 1: Not viewing an offer is not a conscious decision and hence not an active rejection of the offer. It represents simply missing the fact that the offer was made altogether. From the perspective of the customer, it is hence not different from "not receiving the offer" . Consequently, for each offer, the population can be divided into two groups. Firstly, those people who viewed the offer. They will be called "offer-aware". In this group, some people will have used the offer and some will consciously not have used it. The other group of non-receivers and non-viewers will be called offer-unaware group.*

*Assumption 2: The people who received the offer were sampled randomly - They are not, for instance, people who already spend a lot where the offer could be considered a reward. This assumption is reasonable because this is an experiment.*

The business questions of Step 1 are answered through descriptive statistics and a Kruskal-Wallis test with Mann-Whitney U tests as post-hoc tests.
For Step 2, a predictive classifier model is built that predicts if a customer will use an offer or not.
The notebook Starbucks-Analysis contains insights from the results of the various analyses.

## References:
References for sources used are at the beginning of each notebook.
References for libraries used:
**numpy**
Harris, C.R., Millman, K.J., van der Walt, S.J. et al. "Array programming with NumPy", Nature 585, 357–362 (2020). DOI: 0.1038/s41586-020-2649-2.

**pandas**
Jeff Reback, jbrockmendel, Wes McKinney, Joris Van den Bossche, Tom Augspurger, Phillip Cloud, … chris-b1. (2021, June 22). pandas-dev/pandas: Pandas 1.2.5 (Version v1.2.5). Zenodo. http://doi.org/10.5281/zenodo.5013202

Data structures for statistical computing in python, McKinney, Proceedings of the 9th Python in Science Conference, Volume 445, 2010, p.56 - 61, editors: Stefan van der Walt and Jarrod Millman. DOI: 10.25080/Majora-92bf1922-00a

**matplotlib/pylab**
J. D. Hunter, "Matplotlib: A 2D Graphics Environment", Computing in Science & Engineering, vol. 9, no. 3, pp. 90-95, 2007. DOI: 10.5281/zenodo.4475376

**scipy**
Pauli Virtanen, Ralf Gommers, Travis E. Oliphant, Matt Haberland, Tyler Reddy, David Cournapeau, Evgeni Burovski, Pearu Peterson, Warren Weckesser, Jonathan Bright, Stéfan J. van der Walt, Matthew Brett, Joshua Wilson, K. Jarrod Millman, Nikolay Mayorov, Andrew R. J. Nelson, Eric Jones, Robert Kern, Eric Larson, CJ Carey, İlhan Polat, Yu Feng, Eric W. Moore, Jake VanderPlas, Denis Laxalde, Josef Perktold, Robert Cimrman, Ian Henriksen, E.A. Quintero, Charles R Harris, Anne M. Archibald, Antônio H. Ribeiro, Fabian Pedregosa, Paul van Mulbregt, and SciPy 1.0 Contributors. (2020) SciPy 1.0: Fundamental Algorithms for Scientific Computing in Python. Nature Methods, 17(3), 261-272.

**os**
Official documentation: https://docs.python.org/3/library/os.html

**seaborn**
Michael L. Waskom, "Seaborn: statistical data visualization", Journal of Open Source Software, volume 6(60), p. 3021, 2021.

**math/itertools**
1. Van Rossum G. The Python Library Reference, release 3.8.2. Python Software Foundation; 2020.

**json**
Official documentation: https://docs.python.org/3/library/json.html

**statsmodels**
Seabold S, Perktold J. statsmodels: Econometric and statistical modeling with python. In: 9th Python in Science Conference. 2010.

**sklearn**
Scikit-learn: Machine Learning in Python, Pedregosa et al., JMLR 12, pp. 2825-2830, 2011.
