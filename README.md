# Komi-Zyrian morphological analyzer
This is a rule-based morphological analyzer for Komi-Zyrian literary standard (``kpv``) of the Komi language continuum (Uralic > Permic). It is based on a formalized description of literary Komi-Zyrian morphology, which also includes a number of dialectal elements, and uses [uniparser-morph](https://github.com/timarkh/uniparser-morph) for parsing. It performs full morphological analysis of Komi-Zyrian words (lemmatization, POS tagging, grammatical tagging, glossing).

## How to use
### Python package
The analyzer is available as a Python package. If you want to analyze Komi texts in Python, install the module:

```
pip3 install uniparser-komi-zyrian
```

Import the module and create an instance of ``KomiZyrianAnalyzer`` class. Set ``mode='strict'`` if you are going to process text in standard orthography, or ``mode='nodiacritics'`` if you expect some words to lack the diacritics (which often happens in social media). After that, you can either parse tokens or lists of tokens with ``analyze_words()``, or parse a frequency list with ``analyze_wordlist()``. Here is a simple example:

```python
from uniparser_komi_zyrian import KomiZyrianAnalyzer
a = KomiZyrianAnalyzer(mode='strict')

analyses = a.analyze_words('Морфологияса')
# The parser is initialized before first use, so expect
# some delay here (usually several seconds)

# You will get a list of Wordform objects
# The analysis attributes are stored in its properties
# as string values, e.g.:
for ana in analyses:
        print(ana.wf, ana.lemma, ana.gramm, ana.gloss)

# You can also pass lists (even nested lists) and specify
# output format ('xml' or 'json')
# If you pass a list, you will get a list of analyses
# with the same structure
analyses = a.analyze_words([['А'], ['Ме', 'тэнӧ', 'радейта', '.']],
	                       format='xml')
analyses = a.analyze_words(['Морфологияса', [['А'], ['Ме', 'тэнӧ', 'радейта', '.']]],
	                       format='json')
```

Refer to the [uniparser-morph documentation](https://uniparser-morph.readthedocs.io/en/latest/) for the full list of options.

### Disambiguation
Disambiguation is not yet available for this language.

### Word lists
Alternatively, you can use a preprocessed word list. The ``wordlists`` directory contains a list of words from a 1.8-million-word [Komi-Zyrian corpus](http://komi-zyrian.web-corpora.net/) (``wordlist_main.csv``), list of analyzed tokens (``wordlist_analyzed.txt``; each line contains all possible analyses for one word in an XML format), and list of tokens the parser could not analyze (``wordlist_unanalyzed.txt``). The recall of the analyzer is 92.2% on literary texts and 89.1% on social media texts.

## Description format
The description is carried out in the ``uniparser-morph`` format and involves a description of the inflection (paradigms.txt), a grammatical dictionary (kpv_lexemes_XXX.txt files), a list of rules that annotate combinations of lexemes and grammatical values with additional Russian translations (lex_rules.txt), and a short list of analyses that should be avoided (bad_analyses.txt). The dictionary contains descriptions of individual lexemes, each of which is accompanied by information about its stem, its part-of-speech tag and some other grammatical/borrowing information, its inflectional type (paradigm), and Russian translation. See more about the format [in the uniparser-morph documentation](https://uniparser-morph.readthedocs.io/en/latest/format.html).
