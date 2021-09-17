# Semantic Wikipedia Search with Transformers and DistilBERT

## Table of contents: 

- [Overview](#overview)
- [🐍 Build the app with Python](#-build-the-app-with-python)
- [🔮 Overview of the files in this example](#-overview-of-the-files-in-this-example)

## Overview

This example shows you how to build a simple semantic search app powered by [Jina](http://www.jina.ai)'s neural search framework. You can index and search text sentences from ProQuest using a state-of-the-art machine learning  [`distilbert-base-nli-stsb-mean-tokens `](https://huggingface.co/sentence-transformers/distilbert-base-nli-stsb-mean-tokens) language model from the [Transformers](https://huggingface.co) library.

| item   | content                                          |
|--------|--------------------------------------------------|
| Input  | 1 text file with 1 sentence per line             |
| Output | *top_k* number of sentences that match input query |

## 🐍 Build the app with Python

Begin by cloning the repo, so you can get the required files. 
```sh
git clone https://github.com/hcss-utils/jinaai
cd jinaai
```

In your terminal,  you should now be located in you the jinaai's folder. Let's install Jina and the other required Python libraries. 

First create virtual environment

```sh
python3 -m venv env
. env/bin/activate
```

Then install dependencies:

```sh
pip install -r requirements.txt
```

If this command runs without any error messages, you can then move onto step two. 

### 📥 Step 2. Download your data to search 

Index your new dataset (put .txt into data folder): `python app.py -t index -d full`

The whole dataset contains about 50k sentences, indexing all of this will take a very long time.
Therefore, we recommend selecting only a subset of the data, the number of elements can be selected by the `-n` flag.
We recommend values smaller than 100000. For larger indexes, the SimpleIndexer used in this example will be very slow also in query time.
It is then recommended to use more advanced indexers like the FaissIndexer.  

### 🏃 Step 3. Index your data

Index your data by running:

```sh
python app.py -t index
```
Here, we can also specify the number of documents to index with ```--num_docs``` / ```-n``` (defult is 10000).

### 🔎 Step 4. Query your indexed data

A search prompt will appear in your terminal after running:

```sh
python app.py -t query
```

See the text below for an example search query and response.
You can also specify the top k search results with ```--top_k``` /  ```-k``` (default is 5)

```
please type a sentence: What is ROMEO
         
Ta-Dah🔮, here are what we found for: What is ROMEO
>  0(0.36). The ROMEO website, iOS app and Android app are commonly used by the male gay community to find friends, dates, love or get informed about LGBT+ topics.

```