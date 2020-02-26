# Assignment 1
## Important notes
**Submission deadline:**
* **Thursday, 12.03.2020**
**Points: 13 + 2bp**

This assignment is meant to test your skills in course pre-requisites:  Scientific Python programming and  Machine Learning. If it is hard, I strongly advise you to drop the course.

Please use GitHub’s [pull requests](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-requests) and issues to send corrections!

You can solve the assignment in any system you like, but we encourage you to try out [Google Colab](https://colab.research.google.com/).

## Assignment text
1. **[1p]** Download data competition from a Kaggle competition on sentiment prediction from [[https://www.kaggle.com/c/sentiment-analysis-on-movie-reviews/data](https://www.kaggle.com/c/sentiment-analysis-on-movie-reviews/data)].  Keep only full sentences, i.e. for each `SenteceId` keep only the entry with the lowest `PhraseId`.  Use first 7000 sentences as a `train set` and the remaining 1529 sentences as the `test set`. 

2. **[1p]** Prepare the data for logistic regression:
	Map the sentiment scores $0,1,2,3,4$ to a probability of the sentence being by setting $p(\textrm{positive}) = \textrm{sentiment}/4$.
	Build a dictionary of most frequent 20000 words.

3. **[3p]** Treat each document as a bag of words. e.g. if the vocabulary is 
	```
	0: the
	1: good
	2: movie
	3: is
	4: not
	5: a
	6: funny
	```
	Then the encodings can be:
	```
	good:                           [0,1,0,0,0,0,0]
	not good:                       [0,1,0,0,1,0,0] 
	the movie is not a funny movie: [1,0,2,1,1,1,1]
	```
    Train a logistic regression model to predict the sentiment. Compute the correlation between the predicted probabilities and the sentiment. Record the most positive and negative words.
    Please note that in this model each word gets its sentiment parameter $S_w$ and the score for a sentence is 
    $$\text{score}(\text{sentence}) = \sum_{w\text{ in sentence}}S_w$$

4. **[3p]** Now prepare an encoding in which negation flips the sign of the following words. For instance for our vocabulary the encodings become:
	```
	good:                           [0,1,0,0,0,0,0]
	not good:                       [0,-1,0,0,1,0,0]
	not not good:                   [0,1,0,0,0,0,0]
	the movie is not a funny movie: [1,0,0,1,1,-1,-1]
	```
	For best results, you will probably need to construct a list of negative words.
	
	Again train a logistic regression classifier and compare the results to the Bag of Words approach.
	
	Please note that this model still maintains a single parameter for each word, but now the sentence score is
	$$\text{score}(\text{sentence}) = \sum_{w\text{ in sentence}}-1^{\text{count of negations preceeding }w}S_w$$

5. **[5p]** Now also consider emphasizing words such as `very`. They can boost (multiply by a constant >1) the following words.
	Implement learning the modifying multiplier for negation and for emphasis. One way to do this is to introduce a model which has:
	- two modifiers, $N$ for negation and $E$ for emphasis
	- a sentiment score $S_w$ for each word 
And score each sentence as:
$$\text{score}(\text{sentence}) = \sum_{w\text{ in sentence}}N^{\text{\#negs prec. }w}E^{\text{\#emphs prec. }w}S_w$$

You will need to implement a custom logistic regression model to support it.

6. **[2pb]** Propose, implement, and evaluate an extension to the above model.

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg3ODAwODM5OV19
-->