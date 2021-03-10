# alt-bitexts
Data and code associated with paper **An Alternative to Thresholding for Margin-Based Bitext Mining** (Alex Jones & Derry Tanti Wijaya, 2021). COMING TO arXiv SOON.

## **Summary**

In this paper, we explore the idea of using bidirectional pre-translation (translating EN sentences to XX and XX to EN) in order to improve performance on the bitext retrieval task. Mining at the *document* level as opposed to searching entire corpora, we show that a voting-based approach which combines signals from the sentence embedding alignments of translated and untranslated texts sometimes outperforms the simpler method of using a similarity score threshold, as in https://arxiv.org/pdf/1812.10464.

We mine using the recently released contextualized cross-lingual sentence embedding model LaBSE (https://arxiv.org/abs/2007.01852), but using margin-based techniques developed by Mikel Artetxe and Holger Schwenk (https://arxiv.org/abs/1811.01136), which incorporate FAISS for accelerated searching. We experiment on the Tatoeba dataset (https://github.com/facebookresearch/LASER/tree/master/data/tatoeba/v1) described in https://arxiv.org/pdf/1812.10464, as well as on the BUCC '17/18 EN-FR train data (https://comparable.limsi.fr/bucc2017/bucc2017-task.html) and on Wikipedia comparable corpora, namely EN-KK and EN-GU. We provide source code needed to perform bitext retrieval on both the Tatoeba data and on comparable corpora, as well as scripts for training NMT models on this "pseudo-parallel" train data mined from comparable corpora. We also provide the comparable corpora from which we mine bitexts, including the pre-translated versions of these corpora, in addition to the resulting sentence pairs we mine for semi-supervised NMT training using the [XLM](https://arxiv.org/abs/1901.07291) model. Lastly, we also provide false negatives and false positives from the BUCC data to highlight the problematic nature of this dataset.

## **Dependencies**

[PyTorch 1.8.0](https://pytorch.org/get-started/locally/) \
[FAISS 1.7.0](https://github.com/facebookresearch/faiss) \
[Sentence Transformers](https://www.sbert.net/docs/installation.html) (See also [Sentence Transformers Github](https://github.com/UKPLab/sentence-transformers)) \
[GoogleAPIClient 2.0.2](https://github.com/googleapis/google-api-python-client) \
[NLTK 3.5](https://www.nltk.org/install.html) \
Typical data science stack: [Numpy](https://numpy.org/install/), [Pandas](https://pandas.pydata.org/pandas-docs/stable/getting_started/install.html)

## **Tatoeba similarity search**

We [provide code](https://github.com/AlexJonesNLP/alt-bitexts/blob/main/source/retrieve_tatoeba_results.ipynb) for replicating our results on the Tatoeba bitext retrieval / similarity search task outlined in the [LASER paper](https://arxiv.org/pdf/1812.10464). We mine on 64 mid-to-low-resource languages using methods outlined in our paper.

## **Bitext mining from comparable corpora**

We [provide code](https://github.com/AlexJonesNLP/alt-bitexts/blob/main/source/retrieve_pairs_from_cc%20(2).ipynb) to replicate our results on mining pseudo-parallel bitexts from paired Wikipedia documents (EN-KK and EN-GU). The methods implemented in this notebook are described in our paper. We also provide [a notebook](https://github.com/AlexJonesNLP/alt-bitexts/blob/main/source/original_sandbox.ipynb) containing original code used in experimentation, more for transparency in regard to our experimentation process than for reproducibility's sake. SCRIPT FOR SEMI-SUPERVISED NMT TRAINING COMING SOON.

## **Data**

The comparable corpora files from which we mine pseudoparallel sentence pairs are found [here](https://github.com/AlexJonesNLP/alt-bitexts/tree/main/ComparableCorporaMaterials). Descriptions of the files are as follows, where "xx" represents either Kazakh/kk or Gujarati/gu in the file name:

* xx_full_paragraph.csv.zip — File containing original set of EN and XX sentences, grouped into documents. Though this is the original corpus we started out with, its contents are stored in orig.en-xx.zip and orig.xx-en.zip, albeit in a different order. Additionally, the texts below have already been preprocessed. **We therefore recommend using the files below instead.**

* orig.en-xx.zip — File containing original EN sentences in EN-XX corpus, NOT grouped by document.

* orig.xx-en.zip — File containing original XX sentences in EN-XX corpus, NOT grouped by document.

* translation.en-xx.zip — File containing *translated* EN sentences, NOT grouped by document.

* translation.xx-en.zip — File containing *translated* XX sentences, NOT grouped by document.

* id.en-xx.zip — File containing DOCUMENT IDs for EN sentences in corpus. **Because we mine at the document level, you must use these IDs to group sentences in the files above for mining procedures to work.**

* id.xx-en.zip — File containing DOCUMENT IDs for XX sentences in corpus.

The mined pseudoparallel sentence pairs themselves may be found [here](https://github.com/AlexJonesNLP/alt-bitexts/tree/main/MinedTrainData) for both EN-GU and EN-KK. The procedures for mining these sentence pairs are described in our paper and implemented [here](https://github.com/AlexJonesNLP/alt-bitexts/blob/main/source/retrieve_pairs_from_cc%20(2).ipynb).

We [also provide](https://github.com/AlexJonesNLP/alt-bitexts/tree/main/BUCC_EN-FR_fp_fn) a sample of false positives and false negatives from mining attempts on the BUCC '17/18 EN-FR dataset using LaBSE, in an effort to echo previously-voiced concerns about the problematic nature of this dataset. We believe many of the sentence pairs labeled as false positives are perfectly valid translations of one another, while many of the flagged false negatives exhibit flaws that may disqualify them from being gold-standard translations. We encourage others to examine these texts and make up their minds for themselves. Although we don't make the BUCC dataset a focus of our paper and the results we report for this reason, one may freely examine the [dozens of techniques we tried](https://github.com/AlexJonesNLP/alt-bitexts/blob/main/source/original_sandbox.ipynb) to improve bitext retrieval performance on this dataset, and see them summarized in Section B in the appendix of our paper.

## **License**

We retain the [same licensing](https://github.com/AlexJonesNLP/alt-bitexts/blob/main/LICENSE) (BSD) as used in the LASER repository. We acknowledge the derivative nature of our work and direct users to contact the originators of the core tools and methods we use for questions regarding fair usage.

## **Citation**

BibTeX citation for our paper COMING SOON. Citations for all referenced papers should be available at links given above. For a full list of relevant works, please see our paper (LINK COMING SOON).
