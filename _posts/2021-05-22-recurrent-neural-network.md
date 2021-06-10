---
layout: post
title: "Recurrent Neural Network"
date: 2021-05-22
---


# Vanilla Feed-forward Neural Network


![feedforward](/assets/2021-05-22-recurrent-neural-network/feedforward.png)

A vanilla feed forward network (FFN) recieves input with a fixed size (e.g. image), and the input is fed through hidden layers and produces outputs.

In a simplified way, FFNs are abtracted into layer levels: input layer, hidden layers, and output layer.

## How can we handle sequential data?

Such as movies, online shopping or speech recognition, the goal is to predict what is the next  given a historical information? e.g. Youtube recommendation based on your watch histories.



## FFN for Sequential data

![ffn-seq-data](/assets/2021-05-22-recurrent-neural-network/ffn-seq-data.png)


1. What if the length of sequential data is not fixed? Input, hidden, and output (red, green, blue recktangle) architecture cannot handle input of variable length. 

2. Also, the order of such sequence may be very useful, but do FFNs can see the order?

A naive approach.

For issue #1, aggregation some groups of sequential data, converting variable-sized data into fixed-sized data: "Deep Neural Networks for YouTube Recommendations." However, some information in the data may be lost.


# Process Sequences

![ffn-seq-data](/assets/2021-05-22-recurrent-neural-network/ffn-seq-data.png)

Features in many tasks have temporal/sequential dependencies.

![rnn](/assets/2021-05-22-recurrent-neural-network/rnn.png)


For example tasks, from left to right,
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


# Recurrent Neural Neworks

RNNs use one single module that encode information given a time/position in temporal/sequential data.

So in each neuraon of RNN, the output of previous time step is fed as input of the next time step.


![pos](/assets/2021-05-22-recurrent-neural-network/rnn-equation.png)

So it is aggregating the hidden state along every timestep following the flow of time (or sequence order).

Note that we are using the same function & parameters here.

![pos](/assets/2021-05-22-recurrent-neural-network/rnn-function.png)

Then, the question is what is the functional form and model architecture?


![pos](/assets/2021-05-22-recurrent-neural-network/rnn-forward.png)

The W weight matrices and hidden representations are in the same variable that is used across the timesteps.

Here, W_hh encodes the hidden representation that is updated previously, and the W_xh the new input, sharing the model capacity to the past information and current input.

The reason to seperate two trainable wight matrices for hidden representation h_(t-1) and time-spceifc text x_(t) is 1) h and x are might not be of the same dimension 2) each weight matrix gets different roles of learning to map contextual content h and the textual content x. That is we give flexible learning room to the RNN models by giving explicitly seperating two heterogeneous inputs.

Also, tangent hyperbolic is used as non-linearity.


### Computational Graph for RNNs?

TO understand, just unroll the recursion in RNNs.

![unroll](/assets/2021-05-22-recurrent-neural-network/rnn-unroll.png)

The current time is t=1. The current input is x_1, where the original input was h0 (initialized by some function). Update the h_0 to h_1, reflecting the new input in the sequence.



![unroll2](/assets/2021-05-22-recurrent-neural-network/rnn-unroll2.png)

And repeat the process, until the sequence ends at t=T.


![unroll3](/assets/2021-05-22-recurrent-neural-network/rnn-unroll3.png)

The most important thing is to keep the weight matrix W be a single variable that is responsible encoding and hence be the updated as the training target.

For example, a text sequence data "I am happy" and current time is 2 (embedding "happy"). Without considering the "I am" that came before encoding the "happy", the target word would not be making a good sense. So we use the W weight matrix across time, they are learning the aggregation accross the time.


### Mana to Many
![unroll4](/assets/2021-05-22-recurrent-neural-network/rnn-unroll4.png)

You can use encoder decoder architecture by employing another weight matrix W'. That is, we can use the h_t for the downstream task, that uses another set of parameters for the target task. (e.g.language model)

However, the computation is not cheap here. The more time passes, backpropagation would be increasing.

### The Training


![unroll5](/assets/2021-05-22-recurrent-neural-network/rnn-unroll5.png)

The label at each time step is given to supvervise the shared weight matrices. Then the entire loss would be the sum of individual losses, that is L1 ~ LT.

### Many to One

This scenario assumes tasks like sentiment analysis. The target size is fixed, not of variable length.

![unroll6](/assets/2021-05-22-recurrent-neural-network/rnn-unroll6.png)

We read the sequence till the end, and the only hidden representation at the final time step is used. That is we assume the variable size information is all aggregated into the final representation.


### Take a Closer Look


![more](/assets/2021-05-22-recurrent-neural-network/rnn-more.png)

Studying backpropagation in RNNs is quite complex. Studying them would not worth the effort, as the first step would be to understand the general backpropagation in LMs or SOTA models.