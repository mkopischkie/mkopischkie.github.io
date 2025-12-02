---
title: "NN: Models/Methods"
permalink: /nn_models/
layout: single
classes: wide
---

Given data as an array of integers, there are multiple models the data could be applied to such as Convolutional Neural Networks (CNNs) and Long-Short Term Memory Networks. A CNN looks to learn from curves and edges in an image matrix. Since each SMILE character was assigned an integer, it didn't feel that the curves or edges would make much sense. Any curves or edges may be somewhat random. Therefore, I decided to use an LSTM which reads an input forwards and backwards to retain context clues. This, to me, made more intuitive sense given the data. For example, if the model sees an oxygen with a lone pair, it will understand that there needs to be more bonds on the other side of the atom. 

![Orig](/assets/images/oxygen_smile.jpg)

Since I chose to use a LSTM, I will give a brief overview of how it works. 

![Orig](/assets/images/lstm_network.jpg)

The network has a memory by using gates to determine which information is added or removed. There are three gates that determine what information gets passed, how it affects the model, and what is stored in long term memory. These gates are the forget, input, and output. 

- Forget Gate: The current input and previous input are passed together through the forget gate, multiplied by weight matricies, and passed through an activation function. Usually, the activation function is the sigmoid which outputs a number between 0 and 1. If the product is close to 0, the input will be forgotten, otherwise, the input is retained.
- Input Gate: Similar to the forget gate, relevant information is filtered in and out using the sigmoid activation function. Then, a candidate state is created with another activation function, tanh, where the values are spread between -1 and +1. The final weight update is made by computing the product of the sigmoid layer and the tanh layer.
- Output Gate: Like the previous two gates, the first layer is a sigmoid that determines what should be used in the gate. Then, a tanh activation layer scales the values between -1 and +1 to make the hidden state for the next input. The hidden state helps generate the output for the next data vector.

With a better understanding of how LSTMs work, I began filtering the inputs. The PubChem BioAssay database contained thousands of entries, but I decided to use 1000 entries. My data contains 1000 representations of chemical compounds with the labels as GHS hazards. The goal is to predict the toxicity of synthetized compounds based solely on the molecular structure. I built a simple LSTM using PyTorch where the sequential model contains an embedding layer, bidirectional, dropout, and a dense layer. The embedding layer means that each integer in the inputs is embedded into an n-directional space. This is helpful to see how similar a word, or in this case an integer, is to another word, or integer. For example, the words yogurt and milk have more similarity and overlap than yogurt and steak. An embedding would ensure that the words yogurt and milk are close together. In my model, I use a 64-dimensional embedding so that each integer is represented as a 64-dimensional vector. 

The bidirectional specification tells the models to read the data vector forwards and backwards, ensuring that each vector is read forwards and backwards to retain context clues. A dropout layer is used to help prevent a neural network from overfitting by randomly selecting a percentage of weights to set to zero for each epoch. Finally, the dense layer uses the softmax axtivation to assign each input 8 probabilities of belonging to a particular class. 

![Orig](/assets/images/lstm_summary.png)

