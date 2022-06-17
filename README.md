## Project Title
Generating a Database for Southern Tati Verbs & Predicting Their Syntactic Features 

## About me and Southern Tati
I am a native speaker of Southern Tati, an Indo-Iranian language in the Indo-European family, which is mainly spoken in the northwestern parts of Iran. I am a linguist from the Tat community of Takestan in Iran, and my main focus has been on the verbs in the Takestani dialect of Tati. 

Southern Tati has been categorized by UNESCO as a "definitely" endangered language, which means its transition to children has been troubled. This project attempts to contribute to the documentation and instruction of Tati as an endangered language.

## Verbs in Tati
Tati verbs are morphologically very rich, meaning that several pieces of meaning (known as morphemes), otherwise standing as separate words, come together in a single word (verb). These pieces join in a verb for the realization of the specific values related to the syntactic features of tense, aspect, modality, polarity, transitivity, voice, person, number, and gender for a particular verb root. For example, having the root ʌ-χʌr 'to drink,' the realization of the features {tense: past, aspect: subjunctive, modality: indicative, causation: non-causative, voice: passive, person-number-gender: third-singular-feminine, polarity: negative} will be ʌ-neˈ-χʌr-den-i-ast-abiɛ in its abstract (unpronounced-yet) form. When these meaning pieces come together in a verb, several phonological changes happen, and this verb is pronounced as ʌneˈeχʌrdinijɛstɛbijɛ. (for linguists: Some of these changes are different vowel harmony changes, vowel and consonant delitions, glide insertion, and palatalization). 

## Goals
I have done this project with three main goals:
(A) Generating a database of all possible Tati verb conjugations (abstract forms before actual pronunciations),
(B) Extracting the pronounced verbs out of their abstract forms,
(C)Predicting the set of features associated with each pronounced verb. 

Below I explain t details related to how I attained these goals.


### (A) Generating the verb database
This step involved a long-term linguistic analysis. First, I made an initial dataset of ~150 base (uninflected) roots that I gatehred in Tati. Then I found the number of classes for each feature in Tati verbs. After that, I found the compatibility among these features and with the roots I had listed. 

Challenge: Features interact with each other: The presence of one feature may impede the use of another feature in verbs. For example, progressive verbs in Tati cannot be negated (unlike English). Therefore, an equivalent of a verb like 'I am eating' exists in Tati, but its negative version, 'I am not eating,' is ungrammatical. In addition, specific features can be used with some verb roots but not others. For instance, there are roots in Tati that can be used in a causative sense, unlike some other toots. For example, 'cause to' and 'go' do not come together in a single verb but 'cause to' and 'eat' do. Third, the forms related to the features interact, and the use of one form may affect another form. For example, verbs starting witha vowel, loose the vowel if they are negated. A big part of my linguistic analysis was finding these feature-form-root compatibilities. 

Then, I made several decision trees to understand the complicated system of Tati verbs, their abstract features, and the forms used to realize those features. The combination of the decision trees, is like a (manual) machine that takes a root, cobines it with a unique set of syntactic features, and puts them together in an inflected but not pronounced-yet verb (aka, abstract, morphological form). Decision trees were beneficial in understanding how each verb is made, starting from a bare root such as 'to eat' to a fully inflected verb using this root such as ʌ-neˈ-χʌr-den-i-ast-abiɛ. 

It was exciting for me to used Python to translate the logic I came up with for the dicision trees, so that I could automate verbs generation: not for one root or a specific feature set but for all roots and for all possible feature sets that are compatible with it. Iterating over all roots and features, I made a dataset of ~ 33000 inflected Tati verbs, but in their underlying, abstract, unpronounced forms. I saved the verbs into a dataset in .csv. This is where things started to become even more exciting for me!


### (B) Extracting the pronounced verbs from their abstract forms
The verbs are not pronounced as a sum of their morphological pieces. Instead, several phonological changes such as deletion, insertion, vowel, and consonant changes due to neighboring sounds occur when the speakers SAY a verb. A simple English example is I+am+go+ing+to, which can be pronounced as 'I gonna.' This part emanates from my linguistics research in the phonology of Tati. 

I used Regular Expression to translate the aforementioned phonological rules to extract the pronounced version of verbs in my dataset. I used several functions, each of which targeted a specific pattern or group of patterns in my datset and manipulated those patterns in a particular ordering of the functions. 

Challenge: Since some RegEx rules use the output of other rules as their input, it is essential to use the regEx functions in the correct ordering. In other words, the phonological chantes 'feed' each other and if some of those rules stay hungry then things break down! :))

### (C) Predicting the feature sets for verbs

This step involved using Machine Learning models ( Multinomial Naive Bayes, Logistic Regression, Decision Trees, and LSTM) for predicting the feature bundles associated with each inflected (pronounced) verb. The direction of the model improvement was from left to right in the list of the models I mentioned. Even Multinomial Naive bayes gave me a very high set of accusacy scores: all above eighty percent. I also used F1 score as a metrics as it is a harmonic "mean" of recall and precission scores. LSTM model worked best in terms of accuracy and it even got an accuracy score of 1 for the feature Causation. This means that all the verbs that are caustive were classifiled as causative correctly. 

Using machine learning, helped me find my ungrammatical verbs, go back to the dataset I generated, change some of the RegEx rules and get better accuracy scores on the later runs of the models. 


This step, using ML, is significant in the documentation of languages on which little data/analysis is available for the gap between what words are made of and how they are pronounced. This means linguistic fieldworkers can use such models to understand the internal complexity of the words they record in the field. Giving a pronounced verb to these models, they can predict, with high predictive power, what syntactic features each verb is inflected for. 

## Author

Neda Taherkhani
Email: neda.tahe[At Sign]gmail.com

Linkedin: https://www.linkedin.com/in/nedata/ 

## Acknowledgments

Acknowledgments go to the Data Science (5) Bootcamp instructor at Nashville Software School, Michael Halloway, for his kind and unconditional help with this program. Michael knew how vital this program had been to me. He kindly met with me regularly to help me in this project. I also appreciate the role of t TAs of this Bootcamp: Veronica Ikeshoji-Orlati and Alvin Wendt.
