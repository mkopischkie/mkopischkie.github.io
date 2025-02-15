---
permalink: /cleaning/
title: "Data Gathering/Cleaning/Exploration"
layout: single
classes: wide
---

## Data Gathering 

The Data Repository for Human Gut Microbiota, [GMrepo](https://gmrepo.humangut.info/home), provides publically available APIs to access their data. I used this website and its corresponding API to gather data on fecal samples associated with a particular condition or neurological disorder. Each fecal sample contains bacteria from the individual's gut microbiome. Visiting the website, I was initially brought a page where I could select a phenotype for the corresponding gut microbiota and filter the information pertaining to each sample, including age, sex, country, etc. 

I will walk through, in detail, how I collected gut microbiota data for individuals with Schizophrenia. The same collection technique was used for Alzheimer's, Parkinson's, Bipolar Disorder, Epilepsy, Depression, and a healthy control group. I filtered each condition by gender to collect the gut microbiota data. The same collection technique was used for male and female samples. For this in-depth walk-through, I will focus my data collection on males with Schizophrenia. After filtering the website, a dataframe came up with each row representing an individual with information on their age, Body Mass Index (BMI), and residing country. A hyperlink embedded in each row gave me the species, genus, and relative abundance data of the individual's microbiome. 

Rather than slowly collecting the relative genus abundance data for each Run ID, I quickly got the necessary information by using the API. After initially filtering, I could download a dataframe as a .tsv file to extract the Run IDs for gut microbiota data for each individual.

With the Run ID's, I could embed the API in a for loop so that it would pull all the genus information on the Run IDs. At this point, printing the genus outputs a data frame corresponding to the first Run ID. It contains information related to the scientific name of the bacteria found in the sample and the relative abundance. Eventually, I want this data frame to have the column titles as the scientific names and the first column containing the Run IDs so that a row represents a sample with a unique Run ID and the relative abundances for the corresponding bacteria. 

Now that I have the bacteria names and relative abundances associated with each Run ID, I want to retain the corresponding information relating to the gender, age, BMI, country, and other diseases/conditions associated with the sample. As this information is kept in the same .tsv file that I downloaded, I can extract it in the same for loop. Then, I can append each Run ID to an empty array that I initialized before my for loop.

Because the genus and health attributes are stored in an array and I want them in a data frame, I initialize a for loop and concatenate each sample below one another so that the health data frame will look like this: 

![Fifth](/assets/images/df1.jpg) 

Now, I want to do the same thing with the genus data frame, but since it is formatted differently, I need to merge the samples together so that the genus data frame will look like this: 

![Sixth](/assets/images/df2.jpg) 

As I stated earlier, I want the Run IDs listed as the first column, so I need to transpose this data frame. After resetting the index and renaming the Scientific Name column to the Run ID column, so it makes sense after transposing, I can start to merge the two data frames together 

![Seventh](/assets/images/df3.jpg) 

I merge the health and genus data frames together based on matching unique Run IDs from the Run ID column. Then I concatenate so that each row has a unique Run ID and I'm left with a data frame of all the Run IDs and corresponding information for males with schizophrenia. 

![Eighth](/assets/images/df4.jpg) 

I repeat this same process for males and females with the phenotypes I specified above. The code I used to gather this data can be found in the API Data Gathering Jupyter notebook posted on my GitHub, linked to the left under my profile. All the data frames created during data gathering and data cleaning can be found on my GitHub, linked to the left, within the Datasets folder. 

## Cleaning

I will walk through the cleaning process using the male schizophrenia data frame I completed while walking through the data collection. After reading in the data frame I created from the data gathering step, I used the df.isnull().sum() command to check for NaN's in each column. No column had NaN values in this example, so I used the df.unique() command to check for outliers for the BMI, Age, and Country. With other data frames that were larger, I used the df.describe() command to check for outliers at the minimum and maximum values. The BMI column had a couple outliers, so I filtered out the outliers, calculated the median BMI for the remaining samples, and replaced the outliers with the median. I excluded the BMI values less than 15 and over 50 from my filter because the age range was between early teenagers and elders. Initially, I tried to make a better guess for the replacement, but with only Age and Country as additional parameters, I didn't want to make any unnecessary assumptions, skewing the data further. 

Next, I used the df.unique() and df.describe() commands to check for outliers in the Age column, and found an age listed as zero. Although it's possible for a baby to have schizophrenia, I confirmed via the GMrepo website that ages listed as 0 also had an "na" beside it. So, I filtered out the 0 age, took the median of the remaining values, and replaced the zero with the median. 

Then, I used the df.unique() command on the Country column to check if there were zeros there too and only found the expected answers, so no cleaning had to be done to this column. 

The Mesh ID column represents the medical ID for other disorders/conditions that the individual may have. I made a dictionary to serve as a key between the ID and the medical terminology to make reading the data frame simpler. 

The ID for schizophrenia is D012559, but there were additional conditions/disorders that patients reported as well. By turning the Mesh ID column into a flattened series and finding the unique values, I could use the dictionary to see the list of conditions/disorders that patients with schizophrenia reported. 

From this information, I created two data frames, one with the Mesh IDs, and the other with the Condition listed out. But first, I wanted to narrow down the bacteria so that the final data frame would hold the most prevalent bacteria. I experimented with the df.value_counts() function and realized that most bacteria only occurred in a hand-full of samples. I filtered these out by summing the number of times that zero occurred for each genus of bacteria. 

I defined a threshold equating to 20% of the data frame. This threshold removed the bacteria that exceeded it. In other words, if a bacteria exceeded the threshold, 80% of the samples did not contain that particular bacteria genus. I saved the new data frame with the most prevalent bacteria genus' as a .csv file for later use.

With the new filtered data frame, I converted the Mesh IDs to a column titled Condition, where the IDs were replaced with the medical condition/disorder. This required reformatting the Mesh IDs, using the dictionary as a key, and applying the replacement to the Mesh ID column. A snippet of the clean data frame with conditions listed, rather than Mesh IDs, is attached below. 

![Clean](/assets/images/clean.jpg) 

## Visualizations 

### Generic Plots

![Parkinsons](/assets/images/generic_parkinsons_graphs.jpg) 

These three graphs illustrate the relative abundance of the most prevalent microbiota in females with Parkinson's, males with Parkinson's, and the ages of males and females within the sample. The first two graphs confirm that there are differences in the gut microbiota composition between males and females with Parkinson's. This information will be useful for the machine learning models to classify or predict Parkinson's based on the gender parameters given. 

![Alzheimers](/assets/images/generic_alzheimers_graphs.jpg) 

These three graphs illustrate the relative abundance of the most prevalent microbiota in females with Alzheimer's, males with Alzheimer's, and the ages of males and females within the sample. The first two graphs confirm that there are differences in the gut microbiota composition between males and females with Alzheimer's. This information will be useful for the machine learning models to classify or predict Alzheimer's based on the gender parameters given. The histogram containing information on the age of the men and women sampled provides interesting information, but with a larger sample size, we could expect these histograms to be normal. 

![Schizophrenia](/assets/images/generic_schizophrenia_graphs.jpg) 

These three graphs illustrate the relative abundance of the most prevalent microbiota in females with Schizophrenia, males with Schizophrenia, and the ages and BMIs of males and females within the sample. The first two graphs confirm that there are differences in the gut microbiota composition between males and females with Schizophrenia. There is a significant increase in the amount of prevalent bacteria within the Schizophrenia samples compared to the Alzheimer's and Parkinson's samples. This information will be useful for the machine learning models to classify or predict Schizophrenia and differentiate it between other neurological disorders, including the ones graphed above. Both the age and BMI graphs are what I would expect them to look like. 

![Bipolar](/assets/images/generic_bipolar_graphs.jpg) 

These three graphs illustrate the relative abundance of the most prevalent microbiota in females with Bipolar Disorder, males with Bipolar Disorder, and the ages and BMIs of males and females within the sample. The first two graphs confirm that there are differences in the gut microbiota composition between males and females with Bipolar Disorder. There is a significant increase in the amount of prevalent bacteria within the Bipolar samples compared to the Alzheimer's and Parkinson's samples, but a similar amount to Schizophrenia. This information will be useful for the machine learning models to classify or predict Bipolar Disorder and differentiate it between other neurological disorders, including Parkinson's and Alzheimer's, but may pose problems when differentiating between Bipolar Disorder and Schizophrenia. Both the age and BMI graphs are what I would expect them to look like. 

![Epilepsy](/assets/images/generic_epilepsy_graphs.jpg) 

Like Bipolar Disorder and Schizophrenia, there are obvious differences between male and female gut microbiota composition with Epilepsy. Interestingly, it appears that more young males suffer from epilepsy than young females. Furthermore, the average BMI of males with Epilepsy is higher than that of females. 

![Healthy](/assets/images/generic_healthy_graphs.jpg) 

The healthy group of individuals serves as a control group to compare the gut microbiota against that of those suffering from neurological disorders. Similar to the Bipolar group, we see that the average BMI for males is slightly higher than that of females. We need data on a healthy control group so that the machine learning models can learn what a healthy gut microbiome looks like so that it can identify an unhealthy microbiome.

![Depression](/assets/images/generic_depression_graphs.jpg) 

Again, there is a large amount of prevalent microbiota with the sample of those suffering from depression. There are still differences between the male and female microbiomes, specifically in the Akkermansia genus, which is one of the most prevalent genus for females, but almost nonexistent for males. However, this could be because there are more females sampled than males, as we can see in the age histogram. 

### Condition - Related Plots 

![Schizophrenia Associated Conditions](/assets/images/schizophrenia_associated_conditions_count.jpg) 

My main purpose for creating these graphs was not only to see how these neurological conditions interact with one another, but to see if any gut-related issues were prevalent. For both males and females with Schizophrenia, irritable bowel syndrome was frequently reported, which serves to demonstrate the relationship between gut health and neurological conditions. 

![Bipolar Associated Conditions](/assets/images/bipolar_associated_conditions_count.jpg) 

These graphs present a pattern between Bipolar Disorder, Depression, and Schizophrenia. It will be important to analyze how similar/different the gut microbiota compositions are between these three conditions. Again, we see that irritable bowel syndrome was again reported as another major condition, alongside constipation. 

![Epilepsy Associated Conditions](/assets/images/epilepsy_associated_conditions_count.jpg) 

For individuals with Epilepsy, constipation was a major complaint. This indicates that Epilepsy could have the strongest correlation with the gut microbiome. It will be important to analyze how the microbiota in individuals with Epilepsy compares to other neurological disorders, and if that means that Epilepsy truly has a stronger correlation with gut health. 

![Depression Associated Conditions](/assets/images/depression_associated_conditions_count.jpg) 

Again, we see the relationship between Depression, Bipolar Disorder, and Schizophrenia. But just behind those relationships, we see reports of irritable bowel syndrome and constipation. For females with these three conditions, many also reported Thyroid Diseases. This is another issues that needs to be addressed with respect to gut health. 

### Word Clouds

![Word Cloud](/assets/images/wordcloud.jpg)

The concise layout of the word clouds allow for clear visualization to interpret the relationship between neurological conditions and common bacteria genus. Bacteroids and Faecalibacterium are the most common genus across the board. And it's clear that some bacteria common for some neurological disorders are not common, or not existent, for others. 

### Overlayed Plots

![Overlay](/assets/images/overlay.jpg)

These plots provide the clearest overview on how microbiota in individuals with neurological disorders differs from the healthy control group microbiota. Every condition has clear differences, which indicates that a machine learning model to classify or predict neurological conditions may be successful. Furthermore, a recommendation system could be built on the data from the models to recommend additional supplements or food to incorporate into a diet. 


