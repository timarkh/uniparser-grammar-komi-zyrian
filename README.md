uniparser-grammar-komi-zyrian
=============================

This is a formalized description of literary Komi-Zyrian morphology, which also includes a number of dialectal elements and spelling variants. The description is carried out in the UniParser format and involves a description of the inflection (paradigms.txt), a grammatical dictionary (kpv_lexemes_XXX.txt files) and a short list of analyses that should be avoided (bad_analyses.txt). The dictionary contains descriptions of individual lexemes, each of which is accompanied by information about its stem, its part-of-speech tag and some other grammatical/borrowing information, its inflectional type (paradigm), and Russian translation.

This description can be used for morphological analysis of Komi texts in the following ways:

1. The Wordlists directory contains output of the analyzer for two word lists, sorted by decreasing frequency. First word list based on the Komi-Zyrian literary corpus (which contains 1.76 million words of contemporary texts), and the second, on the Komi-Zyrian social media corpus (1.85 million words). Each line of the analyzed word lists contains all possible analyses of a token in XML. The simplest solution is to use these lists (concatenated) for analyzing your texts. The recall of the analyzer is currently 92.2% on literary texts and 89.1% on social media texts. Additionally, this folder contains tokens that could not be analyzed by this analyzer (...-unparsed.txt).

2. The Analyzer directory contains the UniParser set of scripts together with all necessary language files. You can use it to analyze your own frequency word list. Your have to name your list "wordlist.csv" and put it to that directory. Each line should contain one token and its frequency, tab-delimited. When you run analyzer/UniParser/analyze.py, the analyzer will produce two files, one with analyzed tokens, the other with unanalyzed ones. (You can also use other file names and separators with command line options, see the code of analyze.py.) This way, you will not be restricted by my word list, but the analyzer works pretty slowly (expect 300-400 tokens per second).

3. Finally, you are free to convert/adapt the description to whatever kind of morphological analysis you prefer to use.

This software is distributed under the MIT license (see LICENSE.md).
