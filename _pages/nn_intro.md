---
title: "NN: Project Introduction"
permalink: /nn_intro/
layout: single
classes: wide
---

Taking inspiration from "Simulating 500 million years of evolution with a Language Model" (Hayes et al.), this project aims to predict GHS hazard classifications with a SMILE encoded molecule as input, with further research aiming to generate new molecules and predict their classifications. A SMILE-encoded molecule is a representation composed of letters and numbers indicating atoms, bond types, and ring structures. The need for this research exists in defense against synthetic biological threats. Databases including PubChem and CHEMBYL exist to track known biological assays along with their classifications. However, if the government were to come across a synthetized biological molecule, it can take days to identify it and the dangers it may posess. The previously mentioned paper uses one-hot-encoding to read the inputs and a Convolutional Neural Network (CNN) to generate predictions and novel molcules. I propose encoding the SMILE inputs by mapping each token to a unique integer and using a Long-Short Term Memory (LSTM) network to predict capabilities. 

The ability to quickly know, or at least predict, synthesized biological threats remains a largerly unanswered question. 
