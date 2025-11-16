# NatHist - Naturalis Historia Data Mining

A Python-based data mining tool for analyzing Pliny the Elder's *Naturalis Historia* using advanced Natural Language Processing with LatinCy.

## Overview

This project processes and analyzes Latin text from Pliny's *Natural History* to extract linguistic data, contextual information, and statistical patterns. It uses spaCy's Latin language model to perform lemmatization, tokenization, and context-aware searching.

## Features

- **Latin NLP Processing**: Utilizes LatinCy's specialized Latin language model (`la_core_web_lg`)
- **Lemma Extraction**: Search for Latin lemmas across the corpus with context
- **Context Windows**: Automatically extracts surrounding context (5 words before, 6 words after) around matched tokens
- **Book/Chapter Tracking**: Identifies and records the exact location of matches in the text
- **Statistical Visualization**: Generate pie charts and bar graphs showing lemma frequency and distribution
- **CSV Export**: Output results to CSV format for further analysis

## Requirements

- Python 3.9.7 (tested on Windows 10)
- Libraries:
  - spacy
  - pandas
  - seaborn
  - matplotlib
  - numpy

## Installation

### 1. Install Dependencies

```bash
pip install spacy pandas seaborn matplotlib numpy
```

### 2. Install Latin Language Model

```bash
pip install https://huggingface.co/latincy/la_core_web_lg/resolve/main/la_core_web_lg-any-py3-none-any.whl
```

For more information on the LatinCy model, consult the [HuggingFace documentation](https://huggingface.co/latincy/la_core_web_lg).

## Usage

The notebook (`dataMining.ipynb`) is organized in the following steps:

### Step I: Extract Data from Text

The `browseNatHist()` function searches for specified lemmas in the corpus:
- Iterates through tokens in the parsed text
- Matches tokens against your search lemmas
- Extracts context (configurable number of words before/after)
- Returns results as a dictionary with location information

**Customization**: Adjust context window sizes by modifying the parameters in lines with `max(0, i - 5)` and `min(len(doc), i + 6)`.

### Step II: Extract Location Information

The `get_book_chapter()` function identifies the book and chapter where each match occurs.

**Note**: This function is hardcoded for *plin.nat.* format. Modify for other texts by changing the bibliographical abbreviation.

### Step III: Search and Process

1. Modify the `search_lemmas` list with Latin lemmas you want to find:
   ```python
   search_lemmas = [('domus',), ('villa',), ('templum',)]
   ```

2. The script creates a DataFrame with:
   - **Lemma**: The searched term
   - **Context**: The surrounding text passage
   - **Book/Chapter**: Location in the text

3. Results are exported to `output_results.csv`

### Step IV: Visualization

The notebook generates:
- **Pie Chart**: Distribution of lemma frequencies
- **Stacked Bar Chart**: Chapter-wise lemma mentions

## Important Notes

- **Use Lemmas, Not Forms**: Search for base forms (e.g., `templum` instead of `templi`, `domi` instead of `domuum`)
- **Punctuation Removal**: The `remove_punctuation()` function cleans text before processing
- **Customization**: Adjust all parameters according to your research needs
- **File Names**: Modify CSV filenames as needed in each step

## Data Format

The input CSV (`naturalisHistoria.csv`) contains:
- **Text**: The Latin text passages
- **Book/Chapter**: Bibliographical reference

## Output

Results are saved to `output_results.csv` with the following columns:
- Lemma
- Context
- Book/Chapter

