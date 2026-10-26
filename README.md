# Derogatory-Slur-Detection-and-Clustering-
RAPT: a span-aware transformer (XLM-RoBERTa) that fuses slur-span and [CLS] embeddings to detect derogatory slur usage in the Slur Corpus (40k Reddit comments). Compared against TF-IDF+LR/SVM and CLS-only baselines, plus text clustering analysis.
Dataset:

⚠️ Content warning: this dataset contains offensive language, including racial, homophobic and transphobic slurs.

This project uses the Slur Corpus (Kurrek, Saleem & Ruths, 2020), a collection of 40,003 Reddit comments, each containing one of three slurs: one racial, one homophobic and one transphobic. The corpus is balanced across the three, with about 13,330 comments each. The comments come from 2,704 subreddits and average about 34 words.

Each comment is annotated by usage type:

Label	Meaning	Count
DEG	Derogatory	20,530
NDG	Non-derogatory (e.g., mention, quotation)	16,727
HOM	Homonym	1,998
APR	Appropriated / reclaimed	553
CMP	Noun compound	189

Task framing: the labels are binarized into DEG (20,530) vs. non-DEG (19,467), a near-balanced split. Six unlabelled rows are dropped. 22% of comments (8,891) have annotator disagreement, which puts an upper bound on achievable accuracy.

Data not included. The raw data contains Reddit usernames, so it is not redistributed here. Obtain it from the original authors and place it at data/kurrek.2020.slur-corpus.csv.

Citation: Kurrek, J., Saleem, H. M., & Ruths, D. (2020). Towards a Comprehensive Taxonomy and Large-Scale Annotated Corpus for Online Slur Usage. Proceedings of the Fourth Workshop on Online Abuse and Harms (WOAH), ACL.
