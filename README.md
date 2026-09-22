# Statistical POS-Tagged Parser — Penn Treebank

A statistical POS tagger (HMM + Viterbi) and PCFG parser trained on the
NLTK Penn Treebank (labeled) corpus, evaluated on 150 sentences collected
from the Daily Mirror online newspaper.

## Requirements
    pip install nltk scikit-learn matplotlib
    python -c "import nltk; nltk.download('treebank')"

## How to run
Open POS_Parser.ipynb and run all cells in order (Kernel > Restart & Run All).

## Folder structure
    POS_Parser.ipynb              the program (code + analysis)
    data/
      daily_mirror_raw.txt        the 150 raw sentences
      daily_mirror_tagged.txt     the 150 hand-tagged sentences (gold standard)
    models/
      hmm_tagger.pkl              trained tagger
      pcfg_grammar.txt            the PCFG parser data
    results/
      predictions.txt             tagger output vs gold
      metrics.txt                 all evaluation metrics
      accuracy_by_section.png     per-section accuracy chart
      confusion_matrix.png        confusion matrix heatmap
    report/
      report.pdf                  the written report

## Results summary
    Overall tagging accuracy : 83.52%
    Baseline (most-frequent) : 79.89%
    OOV rate                 : 13.71%

## Dataset
The NLTK Penn Treebank (labeled) dataset was used for training, as instructed.