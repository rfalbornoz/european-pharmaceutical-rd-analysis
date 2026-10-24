# European Pharmaceutical R&D Analysis

An unsupervised and unstructured data analysis of the European Medicines Agency (EMA) drug authorization landscape (team project title: "European Drugs Development") — exploring how regulatory pathway flags co-occur, how they relate to authorization outcomes, and how human and veterinary medicines structurally differ.

**Course:** BA820 — Unsupervised and Unstructured Machine Learning (MSBA)
**Section / Team:** A1, Team 10
**Institution:** Boston University, Questrom School of Business

## Team Members

- Samuel Buelvas
- Chamnan Suon
- Gurveen Rekhi
- Roberto Albornoz

## Project Overview

Drug development in Europe shapes the global pharmaceutical industry. By identifying patterns in how the European Medicines Agency (EMA) routes medicines through regulatory pathways, we can surface structural insights that help companies design better authorization strategies and risk profiles for new drug candidates.

The dataset covers **1,988 medicines** reviewed by the EMA — **1,706 human** and **282 veterinary** — with attributes spanning regulatory pathway flags (orphan, biosimilar, generic, conditional approval, accelerated assessment, exceptional circumstances, additional monitoring), authorization outcomes (authorized / withdrawn / refused), therapeutic areas, ATC codes, and pharmacotherapeutic groups.

The project unfolds across four milestones, beginning with individual exploratory questions and converging on a unified market-basket framework that ties regulatory bundles to refusal and withdrawal outcomes.

## Domain Questions

1. **Pathway Co-occurrence (Gurveen)** — Which regulatory pathways co-occur most consistently, and do these bundles remain stable over time?
2. **Approval Trends (Samuel)** — How do regulatory pathway and therapeutic area combinations relate to authorization behaviors over time?
3. **Refusal Drivers (Chamnan)** — What is the association between regulatory pathways and medicine refusal outcomes?
4. **Human vs. Veterinary Structure (Roberto)** — How do regulatory pathways differ between human and veterinary medicines, and how should veterinary features be re-engineered for meaningful segmentation?

## Methods

- **Hierarchical Clustering** with Jaccard distance for categorical/binary feature spaces
- **K-Means Clustering** on engineered numeric features (used selectively after Milestone 2 feedback)
- **Association Rule Mining / Apriori** for frequent itemset discovery and rule generation (Support, Confidence, Lift, Leverage)
- **Market Basket Analysis** treating each medicine as a "basket" of regulatory flags
- **Fisher's Exact Test** for validating structural differences between human and veterinary populations
- **Silhouette Analysis & Elbow Method** for cluster validation
- **Feature Engineering** — multi-hot encoding of pharmacotherapeutic groups, ATC codes, and species categories

K-modes was attempted but removed because frequent pathway combinations (e.g., `orphan_medicine` + `additional_monitoring`) dominated centroid formation and obscured rarer but meaningful patterns.

## Key Findings

- **Pathways behave as bundles, not isolated switches.** Orphan designation, accelerated assessment, conditional approval, and exceptional circumstances co-occur in consistent combinations — regulators evaluate applications holistically.
- **Additional monitoring is the regulatory hub.** Specialized pathways strongly imply additional monitoring (e.g., conditional approval → additional monitoring at confidence ≈ 0.92, lift ≈ 4.04), but the reverse is weak.
- **Orphan designation carries elevated refusal risk.** Apriori on a low-support refusal-discovery run surfaces orphan → refused with ≈ 3× lift over baseline refusal rate, robust across support thresholds (0.005 and 0.003).
- **Monitored medicines are withdrawn less.** Additional monitoring shows below-baseline association with withdrawal (lift < 1.0, negative leverage), suggesting monitored profiles are more stable post-authorization.
- **The veterinary market is structurally homogeneous.** Special approval flags (orphan, additional monitoring, conditional approval) are nearly absent in veterinary medicines (Fisher's exact p-values from 1.1e-03 to 2.7e-29). Clustering collapses to a single baseline, so segmentation requires species-group stratification and market basket "regulatory recipes" instead.
- **Clustering alone is insufficient.** Drug profiles overlap continuously rather than separating into clean groups; meaningful structure emerges only when combining pathway, therapeutic, and outcome signals through association-rule frameworks.

## My Contribution

As a member of Team 10, my contributions spanned data engineering, structural analysis of the human-versus-veterinary populations, cross-team methodological integration, and the pivot to Market Basket / Association Rules as the project's defining analytical framework.

**Data preprocessing and feature engineering**
- Built a consistent preprocessing pipeline that transforms the raw EMA dataset into analysis-ready tables, used across the team's downstream workflows.
- Created derived analytical fields to enable clustering, segmentation, and association-rule analyses.
- Applied multi-hot (binary) encoding to regulatory and therapeutic attributes to produce an analysis-ready feature matrix; used frequency filtering on encoded attributes to reduce sparsity-driven noise.

**Human vs. veterinary structural analysis**
- Designed and executed the comparative analysis of regulatory pathway distributions between the human (n = 1,706) and veterinary (n = 282) medicine populations.
- Built contingency tables by medicine type × pathway category and applied **Fisher's Exact Test** under sparse counts, validating the statistical significance of structural differences (p-values ranging from 1.1e-03 to 2.7e-29).
- Engineered an analysis-ready veterinary feature space and consolidated species into clear, interpretable market segments.
- Applied association mining and clustering diagnostics to identify species-specific regulatory "bundles," and used Jaccard-distance hierarchical clustering on binary pathway vectors to test whether stable veterinary subgroups exist.

**Cross-team methodological integration**
- Unified the four domain questions into a single end-to-end research storyline for Milestones 3 and 4.
- Consolidated and aligned team methods by prioritizing techniques suited to sparse, categorical regulatory data.
- Documented clustering failure modes where dominant categories masked rare-but-important patterns, and used these findings to justify deprioritizing clustering and shifting emphasis toward association-rule mining.

**Pivot to Market Basket / Association Rules (Apriori)**
- Led the methodological pivot for the human-medicines analysis from clustering to Market Basket / Association Rules by representing each medicine as a regulatory "basket."
- Performed Apriori-based frequent-itemset discovery and rule mining both overall and stratified by species, with constraints on maximum itemset size to control combinatorial growth, and rule-directionality constraints to focus on interpretable pathway-to-pathway and pathway-to-outcome relationships.
- Evaluated rules using standard metrics (Support, Confidence, Lift) to rank and filter results.
- Extended baskets with mutually exclusive outcome labels to enable outcome-linked association mining, and conducted a targeted low-support search to surface rare refusal-related rules that would have been missed under standard thresholds — the analysis that produced the orphan → refused finding with ≈ 3× lift over baseline.

**Robustness and sensitivity analysis**
- Performed robustness and sensitivity testing by varying minimum-support thresholds across multiple configurations and re-running key mining setups, confirming that the project's core patterns and conclusions were stable across parameter choices.

## Tools and Technologies

- **Python** (pandas, NumPy, scikit-learn, scipy)
- **Association rule mining**: mlxtend (apriori, association_rules, TransactionEncoder)
- **Statistical testing**: scipy.stats (Fisher's Exact Test, contingency tables)
- **Clustering**: scikit-learn (KMeans, AgglomerativeClustering), scipy.cluster.hierarchy
- **Visualization**: matplotlib, seaborn
- **Environment**: Jupyter Notebook

## Data Source

European Medicines Agency (EMA) public dataset of authorized, refused, and withdrawn medicines reviewed under EU regulatory pathways. The dataset is publicly accessible through the EMA's open data portal.

## Course Context

**BA820 — Unsupervised and Unstructured Machine Learning** is a core course in the Boston University MSBA program at the Questrom School of Business. The course covers clustering, dimensionality reduction, association rule mining, and text mining techniques applied to real-world business problems, with a focus on cases where labeled training data is unavailable or the goal is structural discovery rather than supervised prediction.

## Original Repository

This is a forked copy maintained for portfolio purposes. The original team repository, including full commit history and contributions from all team members, can be found at [SChamnan/Unsupervised-ML---European-Drugs-Development-Analysis](https://github.com/SChamnan/Unsupervised-ML---European-Drugs-Development-Analysis).

## Other Projects

- [Mortgage Prepayment Across Rate Regimes](https://github.com/rfalbornoz/mortgage-prepayment-rate-regimes): individual capstone research paper modeling voluntary prepayment on Freddie Mac loan-level data (2018 and 2020 vintages) with a cross-regime model transfer test.
- [Loan Default Risk Prediction](https://github.com/rfalbornoz/loan-default-risk-prediction): supervised ML pipeline (logistic regression, decision tree, random forest, XGBoost) on LendingClub data for New England and New York (team project).
- [Massachusetts Loan Default Risk](https://github.com/rfalbornoz/analytics-massachusetts-loan-risk): descriptive and geospatial analysis integrating LendingClub loans with ACS Census estimates (team project).
