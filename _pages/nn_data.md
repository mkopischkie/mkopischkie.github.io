---
title: "NN: Data Gathering/Cleaning"
permalink: /nn_data/
layout: single
classes: wide
---

I gathered the data from PubChem by navigating to the BioAssay tab and downloading the concise CSV files. These files contained the SMILES molecular representations. Then, I used the PubChem API to download JSON files with information such as molecular weight, heavy atom count, and GHS hazard classification. For this experiment, I merged the data with SMILE representations and the hazard classification. An example of a SMILE representation is pictured below. 

image

SMILE is a vocabulary that has a grammar, so we can understand that 'C' is different than 'CCCCCC'. If we map the tokens comprising the grammar to integers, we can obtain an array of numbers. 

image

Each number corresponds to a unique token, so a model could read the array as a sentence. First, I had to pad the arrays because a neural network requires all inputs to be the same length. Now, the first input looks like this:

image

The labels that correspond to each data vector need to be cleaned up, so I remove the rows where the label doesn't make sense. For example, I'm expecting a label similar to 'Irritates skin', so I'll remove non-descriptive labels like 'Warning'. Then, I group labels that essentially say the same thing together. For example, I merged the labels 'Toxic if inhaled' and 'Toxic if inhaled or swallowed' into 'Toxic if inhaled or swallowed'. I did this because most likely, the compounds with those two warnings will have very similar functional groups that the model may have difficulty differentiating with limited training data. After merging, some labels only occured twice in the dataset, so I removed them complete to refrain from duplicating samples or generating new ones. Finally, I was left with 14 unique labels. 

image
