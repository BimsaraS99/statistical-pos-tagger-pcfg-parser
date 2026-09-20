# Statistical POS-Tagged Parser — Penn Treebank

A statistical Part-of-Speech tagger and PCFG parser trained on the
NLTK Penn Treebank (labeled) corpus, evaluated on 150 sentences
collected from the Daily Mirror online newspaper.

## Requirements

    pip install nltk scikit-learn matplotlib
    python -c "import nltk; nltk.download('treebank')"

## How to run

Open `POS_Parser.ipynb` and run the sections in order (Restart & Run All).
The notebook reads from `data/` and writes its outputs to `models/` and
`results/`.

## Folder layout

    POS_Parser.ipynb      the program (all code + analysis)
    data/                 the 150 sentences (raw + gold-tagged)
    models/               the trained tagger and the PCFG parser data
    results/              predictions, metrics, confusion matrix
    report/               the written report

## Dataset

The NLTK Penn Treebank (labeled) dataset is used for training, as
instructed in the assignment brief.
