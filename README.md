European Drugs Development

An unsupervised and unstructured data analysis of the European Medicines Agency (EMA) drug authorization landscape — exploring how regulatory pathway flags co-occur, how they relate to authorization outcomes, and how human and veterinary medicines structurally differ.

Course: BA820 — Unsupervised and Unstructured Machine Learning (MSBA)
Section / Team: A1, Team 10

Team Members
Samuel Buelvas
Chamnan Suon
Gurveen Rekhi
Roberto Albornoz

Project Overview
Drug development in Europe shapes the global pharmaceutical industry. By identifying patterns in how the European Medicines Agency (EMA) routes medicines through regulatory pathways, we can surface structural insights that help companies design better authorization strategies and risk profiles for new drug candidates.
The dataset covers 1,988 medicines reviewed by the EMA — 1,706 human and 282 veterinary — with attributes spanning regulatory pathway flags (orphan, biosimilar, generic, conditional approval, accelerated assessment, exceptional circumstances, additional monitoring), authorization outcomes (authorized / withdrawn / refused), therapeutic areas, ATC codes, and pharmacotherapeutic groups.
The project unfolds across four milestones, beginning with individual exploratory questions and converging on a unified market-basket framework that ties regulatory bundles to refusal and withdrawal outcomes.

Domain Questions
Pathway Co-occurrence — Which regulatory pathways co-occur most consistently, and do these bundles remain stable over time?
Approval Trends — How do regulatory pathway and therapeutic area combinations relate to authorization behaviors over time?
Refusal Drivers — What is the association between regulatory pathways and medicine refusal outcomes?
Human vs. Veterinary Structure — How do regulatory pathways differ between human and veterinary medicines, and how should veterinary features be re-engineered for meaningful segmentation?

Methods
Hierarchical Clustering with Jaccard distance for categorical/binary feature spaces
K-Means Clustering on engineered numeric features (used selectively after Milestone 2 feedback)
Association Rule Mining / Apriori for frequent itemset discovery and rule generation (Support, Confidence, Lift, Leverage)
Market Basket Analysis treating each medicine as a "basket" of regulatory flags
Fisher's Exact Test for validating structural differences between human and veterinary populations
Silhouette Analysis & Elbow Method for cluster validation
Feature Engineering — multi-hot encoding of pharmacotherapeutic groups, ATC codes, and species categories
