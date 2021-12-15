# README

## Background: This is the final project for the Udacity Data Science Nanodegree. It is currently WIP. I am currently in the data wrangling stage.

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

If Starbucks wants to send out offers in the future, it is relevant for them to know which offers are worth sending and to whom. The basic task is to use the data to identify which groups of people are most responsive to each type of offer, and how best to present each type of offer.

## Business questions

The analysis needs to answer the following sets of questions:

**Stage 1: Relevance of offers**
* Q1.1: Are the different offer types successful?
* Q1.2: Are there differences in success of different offer types?
* Q1.3: Do certain offer attributes influence the success?

If certain offers are successful (Q1.1), they should be further analysed to understand which demographic groups are particularly likely to react positively:

**Stage 2: Targeting**
* Q2.1: Based on demographic information, which customer is how likely to react to a certain offer type?
* Q2.2: Based on demographic information, which customer is how likely to react to certain offer attributes?

## Data:
Three datasets are provided:
* portfolio, which provides information on the offers
* profile, which provides information on the customers (e.g. demographics)
* transcript, which provides information on events (transact, receive offer, view offer, complete offer)
All three datasets need to be combined to answer the key questions.

## Data wrangling:
The transcript data requires elaborate wrangling. This is due to the fact that one consumer can have multiple active offers at the same time. These offers can in fact be the same offer. Data wrangling will enable us to distinguish which view and complete events belong to which original received offer, and which transactions should be allocated to which offer.

## Analysis
Various assumptions need to be made prior to analysing the data:
*Assumption 1: Not viewing an offer is not a conscious decision and hence not an active rejection of the offer. It represents simply missing the fact that the offer was made altogether. From the perspective of the customer, it is hence not different from "not receiving the offer" . Consequently, for each offer, the population can be divided into two groups. Firstly, those people who viewed the offer. They will be called "offer-aware". In this group, some people will have used the offer and some will consciously not have used it. The other group of non-receivers and non-viewers will be called offer-unaware group.*

*Assumption 2: The people who received the offer were sampled randomly- They are not, for instance, people who already spend a lot where the offer could be considered a reward. This assumption is reasonable because this is an experiment.*

Approaches for analysis could be:
* Stage 1: Multiple t-tests with Bonferroni adjustment or GLM.
* Stage 2: Predictive modelling with hyperparameter optimization to predict likelihood of offer uptake or avg. daily spend when an offer x is sent out to a customer.

## Success Metrics
The following metrics will be used as measures of success or as dependent variables in the various analyses:

* **Spend**: Type continuous. Money spent on avg. per day during aware and unaware states.

* **Offer uptake**: Type binary. Not for informational offer unless a proxy is found for what determines "uptake". This variable is coded 0 for "viewed, but not used" and 1 for "used".

## Population - Defining control and treatment group

For each offer, the sample can be divided into 5 groups:
* **A.** Not received (offer-unaware)
* **B.** Received, not viewed (offer-unaware)
* **C.** Received, not viewed, used (offer-unaware)
* **D.** Received, viewed, not used (offer-aware)
* **E.** Received, viewed, used (offer-aware)

To answer the business questions, different subsets will be needed and compared.
There are two ways of logically splitting the population into control and treatment group. On the one hand, one could define A as control group and B,C,D and E as treatment groups, because A is the only group that did not receive the offer, i.e. the treatment. A is hence also the only group that the company did not invest any money in, as sending out the offer comes at a cost. To understand its return on investment, the company would have to use this split. On the other hand, one could define A, B and C as the control group, as lack of offer awareness from the customers point of view is no different to not receiving the offer. Therefore, this split more authentically reflects consumer behaviour and the difference in behaviour between the groups reflects the attractiveness of the offer.

I argue that the second option of defining the groups is preferable. It neglects the immediate financial considerations of the company, but is more future-oriented. Experiments are carried out to optimize for the future.

As this is a first experiment, one can assume that the company has not yet optimized consumer targeting. In fact, optimizing consumer targeting is an aim of this study. The company will gradually become better at targeting responsive customers. Groups B, C and D will hence shrink in size. Assessing the offer success by comparing A to B-C-D-E in this experimental scenario with sub-optimal consumer targeting cannot reflect the true success of an offer. If for instance offer A was sent out to 1000 consumers and by chance 80% were in group B, C or D, whereas offer B was sent out to 1000 consumers and only 20% were in group B, C or D, offer A would likely appear less successful than offer B. In order to select the truly successful campaign, one must compare the unaware to the aware consumers, because only the aware consumers could judge if an offer is attractive enough to change their purchasing behaviour for it.
