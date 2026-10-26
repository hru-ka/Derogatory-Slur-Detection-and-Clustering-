# Derogatory-Slur-Detection-and-Clustering-
DATASET
-------
Slur Corpus (Kurrek, Saleem & Ruths, 2020), 40,003 annotated Reddit comments.
Not included in this submission due to its size / distribution terms — download
it yourself and place the CSV file in the same folder as the notebook:

    kurrek_2020_slur-corpus.csv

Source: https://github.com/networkdynamics/slur-corpus

REQUIREMENTS
-------------
Python 3.9+ and the following packages:

    pip install torch transformers scikit-learn pandas matplotlib nltk ipywidgets

No NLTK data downloads are required — only the Porter stemmer is used, which
is a pure algorithm and needs no corpus download.

The transformer model (xlm-roberta-base) is downloaded automatically from
Hugging Face the first time the notebook runs — an internet connection is
required for that one-time download (~1.1 GB).

Recommended: run in Jupyter Notebook, JupyterLab, or VS Code with the Jupyter
extension, so the interactive classifier widget (Section 9) renders correctly.


HOW TO RUN
-----------
1. Place kurrek_2020_slur-corpus.csv in the same folder as
   text_mining_rapt.ipynb.

2. Install the requirements above.

3. Open text_mining_rapt.ipynb and run all cells from top to bottom
   (Kernel > Restart & Run All, or Run > Run All Cells).

4. Optional settings, both near the top of Section 1:
   - SAMPLE_SIZE (default 8000): number of rows to train on. Set to None
     to use the full 40,003 rows (slower, but more thorough).
   - DROP_DISAGREEMENT (default False): set True to drop rows where
     annotators disagreed on the label (~22% of the data), for cleaner
     but fewer training examples.

5. Expected running time: roughly 10-20 minutes on a laptop CPU for the
   default 8,000-row sample (4 epochs each for RAPT and the CLS-only
   baseline); a few minutes on a GPU.


WHAT EACH SECTION OF THE NOTEBOOK DOES
----------------------------------------
1.   Load and preprocess the dataset, class balance plot
1b.  Classical preprocessing + TF-IDF baseline (Logistic Regression, SVM)
2.   Tokenizer and slur-span index helper
3.   PyTorch Dataset and collate function
4.   Models: RAPT (span-aware) and the CLS-only baseline
5.   Training and evaluation functions
6.   Run Task 1 (classification) with RAPT, plus training curves and a
     confusion matrix
7.   Run the CLS-only baseline for comparison
7b.  Four-way comparison chart (TF-IDF x2, CLS-only, RAPT)
8.   Run Task 2 (clustering): k-means on RAPT's embeddings, ARI,
     silhouette score, and a PCA visualization
9.   Interactive classifier: type a sentence and get a live
     DEG / non-DEG prediction from the trained RAPT model


OUTPUTS PRODUCED BY THE NOTEBOOK
-----------------------------------
- best_rapt.pt              trained RAPT model weights
- best_cls_baseline.pt      trained CLS-only baseline weights
(these are checkpoint files created when the notebook is run; not included
in this submission)


KNOWN LIMITATION
-------------------
The trained model does not reliably handle negation (e.g. it may still
predict "derogatory" for "he is NOT a [slur]"). This is a known failure
mode in hate-speech classifiers, discussed in Section 8 (Discussion and
Limitations) of the report, and is not a bug in the code.


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
