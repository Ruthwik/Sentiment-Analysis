# Sentiment Analysis using Stanford CoreNLP

This is a Java project for Sentiment Analysis using Stanford CoreNLP.

The [Stanford CoreNLP](https://nlp.stanford.edu/) provides statistical NLP, deep learning NLP, 
and rule-based NLP tools for major computational linguistics problems, 
which can be incorporated into applications with human language technology needs..

 
### Sentiment Analysis

The underlying technology of this is based on a new type of Recursive Neural Network that builds on top of grammatical structures.

The Java documentation for stanford nlp can be found [here](https://nlp.stanford.edu/nlp/javadoc/javanlp/).

The [live](http://nlp.stanford.edu:8080/sentiment/rntnDemo.html) Demo of Stanfod sentiment analysis.


## How to build this project

1. Download the project and import into Eclipse

2. Set the build path which must have the following libraries 

 * stanford-corenlp-3.8.0
 * ejml-0.23
 * stanford-corenlp-3.8.0-models

```
Note: The stanford-corenlp-3.8.0-models has all the trained models. It is not set in the build path of this project due to size constraint. 
Download the jar file from Stanford NLP site
```
3. Run the MainApp.java file

All the dependencies can be downloaded from Stanford NLP [site](https://stanfordnlp.github.io/CoreNLP/) .

## Code Explained
### Initialize

```Java
 // creates a StanfordCoreNLP object, with POS tagging, lemmatization, NER, parsing, and sentiment
props = new Properties();
props.setProperty("annotators", "tokenize, ssplit, parse, sentiment");
StanfordCoreNLP pipeline; = new StanfordCoreNLP(props);
```


### How to find the sentiment score

Run the Annotators on the text and then get the SentimentAnnotatedTree
```Java
// this is the parse tree of the current sentence
Tree tree = sentence.get(SentimentCoreAnnotations.SentimentAnnotatedTree.class);

//print the sentiment score using RNNCoreAnnotations
System.out.println("Sentiment Score: " + RNNCoreAnnotations.getPredictedClass(tree));
```

### How to find 5 classes of sentiment classification: very negative, negative, neutral, positive, and very positive.
```Java
// this matrix contains the confidences
SimpleMatrix sm = RNNCoreAnnotations.getPredictedClass(tree);
```
The estimated probability/confidence looks something like this from 'sm' object

```
Type = dense , numRows = 5 , numCols = 1
 0.111  
 0.758  
 0.087  
 0.035  
 0.009
```

### Output

This project has the following output
```
Sentiment Score: 1.0%
Sentiment Type: Negative%
Very positive: 2.0%
Positive: 12.0%
Neutral: 25.0%
Negative: 52.0%
Very negative: 10.0%
```

