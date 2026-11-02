# Bank Marketing Intelligence

### Explainable Machine Learning for Smarter Customer Targeting

**Project status:** Planning and dataset approval  
**Domain:** Applied Machine Learning · Classification · Business Analytics · Explainable AI

## Table of contents

- [Overview](#overview)
- [Research question](#research-question)
- [Dataset](#dataset)
  - [A critical data-quality issue: leakage](#a-critical-data-quality-issue-leakage)
- [Proposed methodology](#proposed-methodology)
- [What makes this project different?](#what-makes-this-project-different)
- [Tools and technologies](#tools-and-technologies)
- [Repository roadmap](#repository-roadmap)
- [Responsible use and limitations](#responsible-use-and-limitations)
- [Data source and attribution](#data-source-and-attribution)
- [Project context](#project-context)

## Overview

Marketing campaigns are expensive when organisations contact large numbers of people who are unlikely to be interested. This project investigates whether machine learning can help a bank prioritise prospective customers who are more likely to subscribe to a term deposit.

Using historical bank marketing data, the project will compare interpretable and ensemble classification models, evaluate their practical usefulness, and investigate how data leakage can produce misleading results.

The goal is **not simply to maximise predictive accuracy**. It is to develop a reproducible, critically evaluated machine learning experiment that addresses a meaningful business decision: **who should be contacted when a marketing team has limited capacity?**

> **Current stage:** Planning stage. No trained models. Dataset chosen

## Research question

**How effectively can machine learning identify customers likely to subscribe to a term deposit using information available before a marketing call, and which approach offers the most useful balance of predictive performance, interpretability and targeting efficiency?**

The experiment will investigate:

1. How do Logistic Regression, Random Forest and a gradient boosting model compare against a simple baseline?
2. Which evaluation metrics best reflect the costs of missed opportunities and unnecessary calls?
3. How effectively can models prioritise likely subscribers when only a limited proportion of customers can be contacted?
4. Which features appear most influential, and what limitations affect the reliability of those explanations?
5. How does including information unavailable at prediction time change apparent model performance?

## Dataset

**dataset:** [Bank Marketing, UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/222/bank+marketing).

The intended file is `bank-additional-full.csv`, which contains **41,188 campaign records**, **20 input variables** and the binary outcome `y` (whether a client subscribed to a term deposit). The records concern phone-based marketing campaigns by a Portuguese banking institution from **May 2008 to November 2010**.

The data includes customer attributes, previous campaign information, contact-related details and economic indicators. The target is:

- `yes`: the customer subscribed to a term deposit.
- `no`: the customer did not subscribe.

### A critical data-quality issue: leakage

The `duration` variable measures the length of the marketing call. It can be strongly associated with the outcome, but it is **not available before the call occurs**. Using it to choose whom to call would therefore give the model information it could not possess at decision time.

Therefore the duration variable shall be excluded, and all other features will be audited for availability at the intended prediction time. (A seperate demonstration of this leakage scenario may be used to demonstrate the influence of unrealistic variavbles)

The historical nature of the dataset will also be considered when interpreting any conclusions about contemporary marketing.

## Proposed methodology

The project will follow eight stages, starting with understanding the customer data and ending with an explanation of what the results mean in practice.

| Stage | What we will do |
| --- | --- |
| **1. Understand the dataset** | Examine what information is available about each customer, check for missing or unusual values, and see how many customers subscribed. |
| **2. Look for patterns** | Create graphs to explore which customer details and campaign factors appear related to subscription decisions. |
| **3. Prepare the data** | Convert information into a format the models can use and deal with missing values where necessary. Make sure the models cannot accidentally learn from information they should not have. |
| **4. Set aside data for fair testing** | Keep some records separate so we can test predictions on customers the models have not learned from. We will also consider the order in which the campaigns took place. |
| **5. Train and compare models** | Start with a very simple prediction method, then test Logistic Regression, Random Forest and a gradient boosting model to see whether more advanced approaches help. |
| **6. Measure how well they work** | Check how often each model makes correct predictions, how many likely subscribers it finds, and how often it recommends customers who do not subscribe. |
| **7. Test a realistic business scenario** | Imagine the bank can only call a limited number of customers. See whether the models can help it choose the most promising people to contact. |
| **8. Explain the findings** | Identify which information seems most useful, where the models make mistakes, and what would need to improve before a bank could rely on the results. |

We will choose the final model based on the evidence from these tests, rather than assuming that the most complicated model is automatically the best. Results will only be added once the experiments have been carried out.

## What makes this project different?

Rather than presenting a single accuracy score, the project is designed around three complementary questions:

- **Is the prediction valid?** Does the experiment avoid data leakage and evaluate performance on genuinely unseen observations?
- **Is the prediction useful?** Would ranking customers make better use of a limited marketing call budget than a simple baseline?
- **Is the prediction understandable?** Can the model's behaviour, errors and limitations be explained clearly enough to support a responsible decision?

These questions are intended to connect model evaluation with real operational decisions, while acknowledging that historical correlations do not prove a system will work in live deployment.

## Tools and technologies

**Planned core stack:** Python, Pandas, NumPy, Matplotlib/Seaborn, scikit-learn, Jupyter Notebook, Git and GitHub.

**Potential additions:** Permutation feature importance, probability calibration, additional model diagnostics and a Streamlit demonstration dashboard.

## Repository roadmap

- [X] Confirm dataset approval and finalise the research question
- [X] Set up reproducible Python environment and project structure
- [ ] Complete data audit and exploratory analysis
- [ ] Implement preprocessing and baseline model
- [ ] Train and validate competing classification models
- [ ] Compare evaluation metrics and targeting scenarios
- [ ] Investigate feature importance, errors and limitations
- [ ] Publish figures, documented findings and reproduction instructions
- [ ] Optional: add an interactive Streamlit application

**Reproduction instructions and results will be added once the first working experiment is committed.** This avoids advertising files, commands or performance figures that do not yet exist.

## Responsible use and limitations

This is an educational and research-oriented project. The dataset is historical, and its patterns may not reflect present-day banking or customer behaviour. Model predictions may also be affected by biased or incomplete records. The analysis will consider relevant fairness, privacy and interpretability concerns, and will not claim that a trained model is ready for real-world deployment without further validation.

## Data source and attribution

Moro, S., Rita, P. and Cortez, P. (2014). *Bank Marketing* [Dataset]. UCI Machine Learning Repository. [https://doi.org/10.24432/C5K306](https://doi.org/10.24432/C5K306)

The UCI dataset is available under the **Creative Commons Attribution 4.0 International (CC BY 4.0)** licence. The dataset belongs to its original contributors; this repository contains an independent analysis and modelling project.

## Project context

Developed as an independent machine learning portfolio project alongside **CMP5367: Artificial Intelligence and Machine Learning** at Birmingham City University. The intention is to demonstrate skills in problem formulation, exploratory data analysis, reproducible modelling, critical evaluation and technical communication.