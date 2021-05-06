---
layout: post
title: "Deep Learning for Natural Language Processing"
date: 2021-05-06
---
# Deep Learning for NLP
I would like to talk about series of topics in Deep Learning for NLP.

1. Deep Learning Basics
2. Word Embedding
3. Recurrent Neural Networks
4. Text Classification
5. Sequence-to-Sequence Model
6. Machine Reading Comprehension
7. Transformer and Self-attention
8. Language Model
9. Graph Neural Networks
10. Knowledge Grounding


## 1. Deep Learning Basics

### Deep Learning vs Machine Learning

Machine Learning

* Input -> Feature Extraction -> Classification -> Output

Deep Learning

* Input -> (Feature Extraction & Classification) -> Output

That is deep learning doesn't care about feature engineering. Let the machine figure it out.


## 2. Word Embedding

### What is Word Embedding?

Encoding text into vectors. e.g. Word2Vec (most popular one), GloVe, FastText

Convert words into nurmeric representation.

The input is text, and the output is vectors.

### Why Word Embedding?

Dimensionality reduction.
Usually into 300 dimension.

Words in vector representation are very useful.

It let numeric operation over words.

Assume the relation in a country and its capital city
e.g. Korea : Seoul = Japan : Tokyo

And we can use the addition or reduction in words.
Korea - Seoul + Tokyo = Japan


### How do we do?

Use RNN, LSTM, GRU


## 3. Recurrent Neural Network

### What are RNNs?

It handles a sequence of words.

The hierarchy in textual information: character -> word -> sentence -> paragraph -> document

It handles information from sentence level to document level.

## 4. Text Classification

Sentiment analysis, paraphrase identification, natural language inference (NLI)

Multi-task Learning

## 5. Sequence-to-Sequence Model

### Attention Mechanism

They don't use the recursive encoding of RNNs.

Machine Translation


## 6. Machine Reading Comprehension

Extractive answers from the passage.

The answer is text span in the given passage. Question is given, the task is to select the text span in the passage, that would be the answer to the question.

A diverse use of attention mechanism

### Attention as Explantion

To build trustworthy AI,

Machine get feedback from Human
Human get an explanation from Machine

So, somehow, we want to know why an AI model behaves in such ways.

Then, it is the developer of such AI who should be responsible for an unexpected machine behavior. Somebody to blame for auto-driving accidents.

### Attention Supervision

We can teach a model not only by data, but by specifying the model which to attend to.

## 7. Transformer and Self-attention

Bigger models than RNNs.

They use self-attention!

Claiming that you don't need recursive encoding for text sequence. You only need to calculate the attention of a sequence against itself.

## 8. Language Model

They suggest Transfer Learning, which pre-train a huge model and finetune the model to fit a specific task.

e.g. GPT, BERT

### Why Pre-training?

Generalization is amazing. They solve it all. Plus, GPT-2, GPT-3 are proving that building a bigger model with bigger data, at some point, the machine is learning something that it's never seen in the data before.


### Beyond BERT?

XLNET: larger model than BERT.
RoBERTa: better training
ALBERT: faster, smaller
Aslo, riends of BERT..
ERNIE: knowledge base
ELMo
Grover
DistilBert: model compression by knowledge distillation.

### Where To User BERT?

A conversational AI
* retriveal selection in muti-turn conversations (chatbot) e.g. Dialogue System Techonologies Challenge (DSTC) for chatbot
* generative model e.g. google asistant, <a href="https://www.youtube.com/watch?v=D5VN56jQMWM" target="target">google duplex</a>




## 9. Graph Neural Networks

We are particularly interested in Knowledge Graphs

Text is unstructurized data.
But graphs are structurized data.

We need to study node embeddings, edge embeddings, or even graph embeddings. How to use them?

* Graph Convolution Networks (GCN)
* Graph Attention Networks (GAT)

Use the knowledge in a graph for better NLP!


## 10. Knowledge Grounding

### Knowledge Base

It became part of NLP. Why? The helps solving NLP problems.

For example, machine reasoning.

They inject some knowledge from KBs into the machine to solve the reasoning problems.

### Knowledge Grounding

Knowledge Base is a high-level resource. Very useful!

Data (text, image) -> Information (pattern, fusion..) -> Knowledge (KBs)

How to make the machine conditioned on the given knowledge base? Grounding is a technique.

