---
permalink: /cleaning/
title: "Data Cleaning/Exploration"
layout: single
classes: wide
---

## Data Gathering 

The Data Repository for Human Gut Microbiota, [GMrepo](https://gmrepo.humangut.info/home), provides publically available APIs to access their data. I used this website and its corresponding API to gather data on fecal samples associated with a particular condition or neurological disorder. Each fecal sample contains bacteria from the individual's gut microbiome. Visiting the website, I was initially brought to the page below. I could select a phenotype for the corresponding gut microbiota, and/or filter out the information pertaining to each sample, including age, sex, country, etc. 

![GMrepo Home](/assets/images/gmrepo_home.jpg) 

I will walk through, in detail, how I collected gut microbiota data for individuals with Schizophrenia. The same collection technique was used for Alzheimer's, Parkinson's, Bipolar Disorder, Epilepsy, Depression, and a healthy control group. I filtered each condition by gender to collect the gut microbiota data. The same collection technique was used for male and female samples. For this in-depth walk-through, I will focus my data collection on males with Schizophrenia. After filtering for the Schizophrenia phenotype and the male gender, I was faced with the following output. 

![Search Result](/assets/images/search_result.jpg) 

Each row represents an individual with information on their age, Body Mass Index (BMI), and residing country. The species, genus, and relative abundance data are available within the Run ID hyperlink. In the hyperlink, I'm directed to the page below. 

![Sample](/assets/images/runid_sample.jpg) 

Rather than slowly collecting the relative genus abundance data for each Run ID, I quickly got the necessary information by using the API. If you noticed in the second image, I could download the data as a .tsv to extract the Run IDs for gut microbiota data for each individual, as done in the code below

![First](/assets/images/firstcode.jpg) 

From that file, I could embed the API in a for loop so that it would pull all the genus information on the Run IDs. 

![Second](/assets/images/secondcode.jpg) 

The if statement within the for loop is telling my computer that if a Run ID does not have any genus information available, to skip that particular sample. At this point, printing the genus outputs a data frame corresponding to the first Run ID. It contains information related to the scientific name of the bacteria found in the sample and the relative abundance. Since the Taxon ID, Rank Level, and Loaded UID are redundant, I drop them from the genus data frame. Eventually, I want this data frame to have the column titles as the scientific names and the first row as the Run ID so that a row represents a sample with a unique Run ID and the relative abundances for the corresponding bacteria. With this in mind, I change the column names and drop any duplicate scientific names. So now my code looks like this: 

![Third](/assets/images/thirdcode.jpg) 

Now that I have the bacteria names and relative abundances associated with each Run ID, I want to retain the corresponding information relating to the gender, age, BMI, country, and other diseases/conditions associated with the sample. As this information is kept in the same .tsv file that I downloaded, I can extract it in the same for loop. Then, I can append each Run ID to an empty array that I initialized before my for loop so that now my code looks like this: 

![Fourth](/assets/images/fourthcode.jpg) 

From now on, I will associate the health data frame/array with the gender, age, BMI, etc. information. Because the genus and health attributes are stored in an array and I want them in a data frame, I initialize a for loop and concatenate each sample below one another so that the health data frame will look like this: 

![Fifth](/assets/images/fifthcode.jpg) 

Now, I want to do the same thing with the genus data frame, but since it is formatted differently, I need to merge the samples together so that the genus data frame will look like this: 

![Sixth](/assets/images/sixthcode.jpg) 

As I stated earlier, I want the Run IDs listed as the first column, so I need to transpose this data frame. After resetting the index and renaming the Scientific Name column to the Run ID column, so it makes sense after transposing, I can start to merge the two data frames together 

![Seventh](/assets/images/seventhcode.jpg) 

I merge the two rows together based on matching Run ID columns, then concatenate so that each row has a unique Run ID and I'm left with a data frame of all the Run IDs and corresponding information for males with schizophrenia. 

![Eighth](/assets/images/eighthcode.jpg) 

I repeat this same process for males and females with the phenotypes I specified above. The code I used to gather this data can be found in the API Data Gathering Jupyter notebook posted on my GitHub, linked to the left under my profile. 

## Cleaning

Steps taken coming soon :)

## Visualizations 

### Generic Plots

![Parkinsons](/assets/images/generic_parkinsons_graphs.jpg) 

![Alzheimers](/assets/images/generic_alzheimers_graphs.jpg) 

![Schizophrenia](/assets/images/generic_schizophrenia_graphs.jpg) 

![Bipolar](/assets/images/generic_bipolar_graphs.jpg) 

![Epilepsy](/assets/images/generic_epilepsy_graphs.jpg) 

![Healthy](/assets/images/generic_healthy_graphs.jpg) 

![Depression](/assets/images/generic_depression_graphs.jpg) 

### Condition - Related Plots 

![Schizophrenia Associated Conditions](/assets/images/schizophrenia_associated_conditions_count.jpg) 

![Bipolar Associated Conditions](/assets/images/bipolar_associated_conditions_count.jpg) 

![Epilepsy Associated Conditions](/assets/images/epilepsy_associated_conditions_count.jpg) 

![Depression Associated Conditions](/assets/images/depression_associated_conditions_count.jpg) 
