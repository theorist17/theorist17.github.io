---
layout: post
title: "Machine Reading Comprehension with Attention"
date: 2021-06-02
---

# Teaching Machines to Read

![oops](/assets/2021-06-02-machine-reading-comprehension/machine.png)

In this post, we're trying to teach machines to read.

![oops](/assets/2021-06-02-machine-reading-comprehension/parse.png)

Should we be analysing the syntactic parse tree? Would such grammar rules extracted be useful for the machines to read?

# Reading Comprehension as Question Answering


![oops](/assets/2021-06-02-machine-reading-comprehension/rc-as-qa.png)

Early in the NLP, an evaluation approach to measure the reading comprehension of mahcines were introduced that let the model read some text and ask them to answer some questions. This still sounds reasonable.


![oops](/assets/2021-06-02-machine-reading-comprehension/rc-as-qa1.png)

Reading comprehension can be casted as a question answering task, that demonstrate the understanding degree of NLP models. Given the input as text passage and the relavant questions, a reading comprehension system should correctly answer them.


![oops](/assets/2021-06-02-machine-reading-comprehension/rc-as-qa2.png)

# Reading Comprehension is a New Field

Before 2015, we hadn't had any statistical NLP systems which is capable of reading a simple passage and answering questions.

![oops](/assets/2021-06-02-machine-reading-comprehension/rc-as-qa3.png)

Before 2015, there were few datasets and systems for reading comprehension. Such datasets had a limited amount of training samples. 


![oops](/assets/2021-06-02-machine-reading-comprehension/rc-as-qa4.png)

By 2015, there were sudden increase in both dataset and reading systems. All of such datasets are very diverse, capturing different aspects of human languages. These days, the regard 100K examples as large these days. 10K sized dataset is regarded as quite small, usually for small research. Regarding the systems, end-to-end deep learning neural networks were introduced!


![oops](/assets/2021-06-02-machine-reading-comprehension/rc-as-qa5.png)

There was rapid progress since then. In SQuAD, which was released in 2016, within several months, machines exceeded humans! (due to the overfitting)

# Outline

![oops](/assets/2021-06-02-machine-reading-comprehension/outline.png)

For the following section, we discuss datasets and model architecture for the machine reading comprehension task.  

# CNN/Daily Mail Datasets

![oops](/assets/2021-06-02-machine-reading-comprehension/cnn.png)

These datasets, provided by DeepMind, contains many document sets, where each sample passage has the average of 4 qeustions. story The highlights on for the article is given as a blank question for model to fill in the missing words. Precisely one entity or word is blanked out for each story highlight.


![oops](/assets/2021-06-02-machine-reading-comprehension/cnn1.png)

This dataset opened a new chapter in machine reading task beyond the machine translation task. They used an entity recognition model to identify well-known entities in the text. Then, they replaced such entities by this entity markers, which are special tokens. For the questions, they reused the highlights replacing some words by a placehoder marker. The goal of this task was to infer which entity refers to the marked placehodler. What a simple and free way to create a large-scale dataset; 380K for CNNs and 879 for Daily Mail.


## Attentive Reader

![oops](/assets/2021-06-02-machine-reading-comprehension/categorical.png)

How to solve the task? They built a symbolic feature vector. By symbolic, we mean something that represent a feature in a catergorical way. In the figure above, linear classifiers are denoted as f, and an embedding as e. They prepared ab embedding e based on the 8 conditioned listed in the box below. Such heuristics are something like co-occurences, Jaccard similarity, etc. What they did was emprically engineer better feature representation. 

But we could build a deep learning model that requires no further feature embedding. This is called this as attentive reader, where they encode question and passage to infer the answer based on their interaction in vector spaces. These are not symblic features, we call them numeric features. 

![oops](/assets/2021-06-02-machine-reading-comprehension/attentive1.png)

Given a question, the attentive reader used a sequential model (bidirecitonal LSTMs) to encode the question into a numeric (hidden) representation to solve the task. 

![oops](/assets/2021-06-02-machine-reading-comprehension/attentive2.png)

Then, attentive reader also used the LSTMs to encode words in the associated passage.

![oops](/assets/2021-06-02-machine-reading-comprehension/attentive3.png)

Finally, attentive reader used attention between a qeustion and all the bidirectional LSTM represetantions for words in a passage. Then the attention probability inferred points out which words are important and should be attended by the attentive reader. Then, aggregating the passage and the attention weights, the output vector is produced, projected via another linear layer to choose the a entity (among entity in the passage). Another attentive model (by DeepMind) were actually first proposed earlier to this version of attentive reader (by Stanford).

![oops](/assets/2021-06-02-machine-reading-comprehension/attentive4.png)

And it's quite messy.

![oops](/assets/2021-06-02-machine-reading-comprehension/attentive5.png)

The Stanford attentive reader was not only simpler but its performance gain were massive.


![oops](/assets/2021-06-02-machine-reading-comprehension/understanding.png)


![oops](/assets/2021-06-02-machine-reading-comprehension/analysis.png)

In many cases, two sentences may have the exact matching text span, or share a sementic between two sentences. The first sentence that include a placeholder is the question sentence and the following sentences are of the context passage. If the system understand that two sentences save a similar meaning, then it should be able to predict the correct entity (entity 3 in the below example).

![oops](/assets/2021-06-02-machine-reading-comprehension/analysis1.png)


In cases of partial clue, there are no explicit evidence that the support the corresponding sentences. To complicate the problem more, the cases of multiple sentences refers when the system is required to answer an entity placed in a paragraph.

So what level of lanugage understanding is needed? People analysed the CNN/Daily Mail datasets and found that the paraphrasing and partial clue were the most frequently observed.

![oops](/assets/2021-06-02-machine-reading-comprehension/analysis2.png)

Data centric approach to improve the neural networks have been spotlighted, instead of model-centric progress. Historically, the progress to construct the benchmark dataset were the major efforts!