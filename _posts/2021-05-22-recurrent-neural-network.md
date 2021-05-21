---
layout: post
title: "Recurrent Neural Network"
date: 2021-05-22
---


# Vanilla Feed-forward Neural Network


![feedforward](/assets/2021-05-22-recurrent-neural-network/feedforward.png)

A vanilla feed forward network (FFN) recieves input with a fixed size (e.g. image), and the input is fed through hidden layers and produces outputs.

In a simplified way, FFNs are abtracted into layer levels: input layer, hidden layers, and output layer.

## How  can we handle sequential data?

Such as movies, online shopping or speech recognition, the goal is to predict what is the next  given a historical information? e.g. Youtube recommendation based on your watch histories.



## FFN for Sequential data

![ffn-seq-data](/assets/2021-05-22-recurrent-neural-network/ffn-seq-data.png)


1. What if the length of sequential data is not fixed? Input, hidden, and output (red, green, blue recktangle) architecture cannot handle input of variable length. 

2. Also, the order of such sequence may be very useful, but do FFNs can see the order?

A naive approach.

For issue #1, aggregation some groups of sequential data, converting variable-sized data into fixed-sized data: "Deep Neural Networks for YouTube Recommendations." However, some information in the data may be lost.

# Recurrent Neural Neworks

## Process Sequences


Features in many tasks have temporal/sequential dependencies.

![ffn-seq-data](/assets/2021-05-22-recurrent-neural-network/ffn-seq-data.png)

From left to right,
1. one-to-one: FFN such as MNIST. Their input/output length has a fixed form. e.g. image size as input and class label as output.
2. one-to-many: here, the input length is fixed, but the output length is variable, e.g. image captioning, movie-to-genre.
3. many-to-one: variable length input for one fixed-sized output. e.g. only the input for sentiment anlaysis is sequential text data.
4. many-to-many: both input/output of variable length (they many not have the same length), e.g. machine translation, POS tagging.


### Image Captioning

Image encoding (CNN) + language model (RNN)

![image-captioning](/assets/2021-05-22-recurrent-neural-network/image-captioning.png)

A famous dataset is MS COCO. This is not object detection! The caption is not one of class, but a variable-length sequence of texts. Very hard to solve this task.

### Sentiment Analysis

A review text is given, classifcy into a finte set of class.


![sentiment](/assets/2021-05-22-recurrent-neural-network/sentiment.png)

### Machine Translation

Source language -> target language (e.g. Korean -> English)

![translation](/assets/2021-05-22-recurrent-neural-network/translation.png)

A huge leap in NNs: Google translate, Naver Papago.


### Part-of-speech (POS) tagging/parsing

Marking a word in a sentence by its role (speech tag).

Improve model's understanding on the language itself.

But recent language models are not that relying on such tagged information.

![pos](/assets/2021-05-22-recurrent-neural-network/pos.png)


## Recur