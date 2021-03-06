# Mod 4 Project: Natural Language Processing (NLP) - Improving online conversation: Use of NLP analysis to build a multi-headed model capable of detecting different types of online discussion toxicity like threats, obscenity, insults, and identity-based hate.


Student name: Andi Osika

* Student pace: part time
* Scheduled project review date/time: June 30, 2020
* Instructor name: James Irving, PhD
* Blog post URL: https://learn.co/blog/blog_posts/26973/edit

## Relevant files: 
  * Improving_Online_Conversation.ipynb
    * Notebook with code, experimentation, visualizations, conclusion, and recommendations (see quicklinks in file section 1.1)
  * NonToxic_Communication.ppt OR NonToxic_Communication.pdf
    * Non-technichal presentation of project, findings, recommentations
   * [Recording of Non-Technical Presentation](https://rebrand.ly/NLP-and-Keras) 
    
    
    
## Deep Learning using Natural Language Proccessing and Recurrant Neural Networks for multi-label multinomial classification with an extremely highly imbalanced dataset.  
    

### Overview: 
The goal of this prjoect was to use NLP analysis to build a multi-headed model capable of detecting different types of online discussion toxicity like threats, obscenity, insults, and identity-based hate.

Since I had little experience with deep learning, that was the method used to classify to gain experience. It proved to be a challenging problem.

There was signficant target imbalance of 10% being amplified needing to categorize 6 overlapping classes. A search indicates that that this problem exists even for experts in the field. One example can be found here where researchers at Stanford experimented with this problem and still seek ways to overcome this challenge.

### Background: 
Freedom of speech is a right.  Digital platforms facilitate conversations, but struggle to do so efficiently while enabling this freedom while minimizing abuse and harrasment that can come with the 'anonymity effect' of a virtual climate.  

Even though the Constitution guarantees the right of free speech, that right is not an absolute one. The law has long recognized specific limitations when it comes to speech, such as prohibitions against slander and libel. 

This dataset is provided by [Conversation AI ](https://conversationai.github.io/) is a collaborative research effort exploring ML as a tool for better discussions online.  The source is a collection of comments from Wikipedia’s talk page edits circa 2017.  The result is a classification list of 159,571 samples provided by Wikipedia and have been labeled by human raters for toxic effects.  These comment classifications can fall into more than one of the following categories:

>The types of toxicity are:
* toxic
- severe_toxic
- obscene
- threat
- insult
- identity_hate


**Warning:** the text found in each of the categories outlined above is extremely offensive. It is important to point out that as the researcher I did not create or support any of the sentiment captured in the toxic language, but feel it important to observe it in order to evaluate findings.
 The supporting visualizations are equally offensive in the notebook.  Because of this, edited versions of some the most offensive findings were/are edited text that I feel conveys the ideas without perpetuating the toxic messages and used for the non-technical explanation.  However the findings in this analysis are necessary for identification's sake.  The intention is to use this type of analysis in order to mitigate situations where others feel unable to share their views at the risk of abuse or feeling that are in harm's way.

### Findings:

In evaluating the toxic text/comments to identify what classified them as such, patterns developed that demonstrated specific words helped in identifying toxicity. In particular, the same three words appared between 75%-100% of the time in four of the categories: Toxic, Severe Toxic, Insulting, and Obscene. More unique words were used in threatening comments and identity-based hate comments. Comment length was also comparitvely evaluated. It was determined that there was little difference in comment lenght between those made with toxic sentiment and those without.


Also it was observed that there was major imbalance in the classes severe toxic, threat, and identitiy hate.  The table below illustrates this.  If a row has a 0 it indicates no target was identified.  A row with a 1 indicates a target was identified:

| Target | Toxic |Severe_Toxic| Obscene	| Threat|	Insult |	Identity_Hate |
|--| ---   | ---        | ---      | ---   | ---      | ---              |    
| 0	|108,232	|118,498|	113,343	|119,310	|113,776	|118,634 |
|1	|1,1446	|1,180	|6335	|368| 5902	|1044|


Several Neural Netowrks were modeled using Keras: https://keras.io/

While varying deep learning models were able to have high rates of accuracy their ability to identify toxic text proved to be more simple than the case of identifying the extremely underclassified examples, with an accuracy of rate of 96% , recall topped out at ~87% in the best case in the multi-class model using deep learning for one category.  In most cases, recall was 0 for the smaller classes. 

### Conclusion:

The best model is as follows:
A Recurrent Neural Network was implemented using an embedding layer of 128 and LSTM Long Short Term Memory and dropout of .25.  to avoid overfitting, an l2regularizer was added with a lambda of .00001. 'Relu' activation was used in the hidden layer and sigmoid on the final.  
In order to address the class imbalance, [Focal Loss](https://focal-loss.readthedocs.io/en/latest/generated/focal_loss.BinaryFocalLoss.html) was implemented, with result in one of the three classes that demonstrated a recall of 0.

rnn_last.add(Dense(25, kernel_regularizer=regularizers.l2(.00001),activation='relu'))
rnn_last.add(Dense(6, activation='sigmoid'))

**3 - Layer RNN with a pattern 50_25_6 : Recall for all True Negatives was .99 - 1.0**

|Classification | Recall|
|-- | --|
|Toxic | .68
|Severe Toxic | **.39**
|Obscene | .78
|Threatening | .0
|Insult | .65
|Identity Hate | .0 


Despite having an overall lower recall in some classes, this model is considered the best model because it was able to predict Severe Toxic comments 39% of the time which is better than any other model.  

It's recommended to use this model to find overall toxic language and develop metrics and associated action plans.  

These findings provided a foundation for future work to:
Simplify the classifications into three classes, toxic, threatening and identity hate and suggest future work to identify these classes.  More data could be collected or undersampling could be implmented to target these groups specifically.
