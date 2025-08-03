# Self Project 
# ARIES-Hackathon
# Publishability Classifier

# Name : Parv Khanna
# Enrollment number : 23112070

The goal was to build an intelligent system capable of analyzing research papers and classifying them as either **publishable** or **non-publishable**, like a scientific reviewer would.
I achieved this using **machine learning techniques** to build a model that is both accurate and explainable.

## Objective
The classifier was trained to distinguish between:

- **Publishable Papers**  
  These are papers that are well-structured, meaningful, and cited as published in the dataset (R006 to R015).
- **Non-Publishable Papers**  
  These papers are intentionally less rigorous, and are not cited as published (R001 to R005). They often lack structure, clarity, or scientific substance.
  
The system is designed to **mimic human reasoning**, providing not just predictions, but also a **plain-language justification** for each result.

## Approach
I chose a **hybrid strategy**, combining handcrafted features with machine learning to deliver robust, interpretable results.

## Step 1: Extracting Key Sections — Introduction and Conclusion
In scientific research papers, the Introduction and Conclusion play a critical role:

- The **Introduction** sets up the motivation, context, and objectives of the work.
- The **Conclusion** wraps up the findings and reflects whether the objectives were achieved.
  
To mimic how a reviewer reads and evaluates a paper, my model focuses on extracting and analyzing these sections.
I used regular expressions to find text between:

- "introduction" and "methodology" (or "methods")
- "conclusion" and "references" (or "acknowledgments")

This allows me to isolate just the content in those two key parts of the paper for further analysis.

## Step 2: Readability & Structure Metrics
I computed several textual quality indicators:

- **Dale-Chall Readability Score** – measures how easy the paper is to understand.
- **Automated Readability Index (ARI)** – estimates school grade level needed to comprehend the text.
- **Word Count** – longer documents may indicate more in-depth analysis.

## Step 3: Semantic Coherence
A paper’s Introduction and Conclusion should be logically aligned.
To measure this, I used a sentence transformer model (**MiniLM**) to generate vector embeddings and compute **cosine similarity** between the intro and conclusion sections. A well-aligned paper should show high similarity.

## Step 4: Text Representation with TF-IDF
I used **TF-IDF (Term Frequency–Inverse Document Frequency)** to capture important keywords and phrases.
I considered **1-grams and 2-grams**, with a feature cap of 2000 for efficiency.

## Step 5: Classification with an Ensemble Model
Instead of relying on a single algorithm, I used a **Voting Classifier** that combines the strengths of:

- **Logistic Regression** (for linear patterns)
- **Random Forest** (for interpretability and non-linearity)
- **Gradient Boosting** (for subtle edge cases)

Each model casts a "vote", and the combined output gives a final prediction with confidence.
Evaluated prediction on the basis of **f1-score, weighted average and macro average.**
## Why This Approach Works
Most models focus only on the text itself.
My approach adds **contextual intelligence** — understanding how a paper is written, how it flows, and how readable it is.
The model is small, fast, and works well on limited data, making it perfect for hackathon deployment.

## Futher Improvement
To improve the model further, I can incorporate section-aware embeddings using SciBERT, which is trained specifically on scientific text. Expanding the dataset through data augmentation or semi-supervised learning would enhance generalization. Fine-tuning classification thresholds and applying advanced ensemble techniques like stacking could also boost performance. Additionally, incorporating citation patterns, figure/table analysis, or abstract based scoring would allow the model to capture more scholarly details, improving its ability to mimic expert level publishing judgment.
