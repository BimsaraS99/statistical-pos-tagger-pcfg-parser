# Statistical POS-Tagged Parser using the Penn Treebank

A statistical Part-of-Speech (POS) tagger and PCFG parser trained on the NLTK
Penn Treebank (labeled) corpus, and evaluated on 150 sentences manually
collected and annotated from the Daily Mirror online newspaper.

The tagger is a Hidden Markov Model (HMM) decoded with the Viterbi algorithm,
extended with a data-driven unknown-word handling mechanism. The parser is a
Probabilistic Context-Free Grammar (PCFG) induced from the treebank's parse
trees.

**GitHub:** https://github.com/BimsaraS99/statistical-pos-tagger-pcfg-parser

---

## Requirements

- Python 3
- The following libraries:

```
pip install nltk scikit-learn matplotlib numpy
```

- The Penn Treebank corpus (downloaded on first run):

```
python -c "import nltk; nltk.download('treebank')"
```

---

## How to Run

1. Install the requirements above.
2. Open `POS_Parser.ipynb` in Jupyter Notebook (or VS Code).
3. Run all cells in order: **Kernel > Restart & Run All**.

The notebook reads its input from the `data/` folder and writes all trained
models to `models/` and all evaluation outputs to `results/`.

---

## Project Structure

```
POS_Parser_Project/
|
├── POS_Parser.ipynb        The main program (all code + analysis)
├── README.md               This file
├── report.docx             The written report
|
├── data/                   Input sentences and annotations
│   ├── daily_mirror_raw.txt          The 150 raw sentences, one per line
│   ├── daily_mirror_template.txt     Tokenised sentences (blank tags) for annotation
│   └── daily_mirror_hand_tagged.txt  150 manually POS-tagged sentences (gold standard)
|
├── models/                 The trained models
│   ├── hmm_tagger.pkl           The trained HMM tagger (saved for reuse)
│   ├── hmm_tagger_readable.txt  Human-readable summary of the tagger's probabilities
│   └── pcfg_grammar.txt         The PCFG parser data (grammar rules + probabilities)
|
└── results/                The evaluation outputs
    ├── metrics.txt               All performance metrics (accuracy, F1, ablation, OOV, parse coverage)
    ├── predictions.txt           The tagger's output vs. gold tags (raw format)
    ├── prediction_results.tsv    Same predictions as a readable table (opens in Excel)
    └── confusion_matrix.png      The confusion-matrix figure
```

---

## Main Results

The tagger was evaluated on the 150 Daily Mirror sentences (2,451 tokens),
compared against the manually annotated gold standard.

| Metric | Result |
|---|---|
| Per-token accuracy | **83.52%** (2047 / 2451) |
| Weighted F1-score | 0.836 |
| Sentence-level accuracy | 9.33% (14 / 150 fully correct) |
| Baseline accuracy (most-frequent tag) | 79.89% |
| Out-of-vocabulary (OOV) rate | 13.71% |
| Accuracy on seen words | 84.40% |
| Accuracy on OOV words | 77.98% |

**Ablation study (contribution of each component):**

| Configuration | Accuracy |
|---|---|
| Baseline (most-frequent tag) | 79.89% |
| HMM + Viterbi (unknown-word clues off) | 75.68% |
| Full model (unknown-word clues on) | **83.52%** |

**Key findings:**
- The full model outperformed the baseline by **+3.63 percentage points**.
- Robust unknown-word handling was the most important component: enabling it
  improved accuracy by **+7.83 points**, and without it the model scored *below*
  the baseline.
- The main source of error was proper-noun recognition (NNP recall 0.665),
  caused by out-of-vocabulary named entities in the out-of-domain news text.
- The PCFG parser reached only 1.3% parse coverage on the news sentences, as a
  single unseen word or structure prevents an entire sentence from being parsed.

---

## Dataset

The NLTK Penn Treebank (labeled) dataset is used for training, as instructed
in the assignment brief. The 150 test sentences were manually collected from
dailymirror.lk across four sections: business (40), politics (40), sport (40)
and local news (30).