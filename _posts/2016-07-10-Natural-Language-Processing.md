---
title:  "Introduction to Natural Language Processing"
date:   2016-07-14 12:58:00
description: Natural Language Processing
---



In this article I'll introduce you to the field of Natural Language Processing. We'll have a look at why **Natural Language Processing** (NLP) is important and briefly discuss the various stages involved in processing of natural language. We'll also have a look at the state of the art of NLP.  

#### What is Natural Language Processing?

It's the ability of systems to process natural language such as English rather than a language that has been designed specifically for computers like C. The system should take in the human speech, process it and derive some meaning out of it. But it's not that easy as it may seem. 

#### Importance of Natural Language Processing

The emergence of this field can be dated back to the 1950s. Alan Turing in 1950 published a paper entitled 'Computing Machinery and Intelligence'. He asserted that a computer could be considered intelligent if it could carry on a conversation with a human being without the human realising that they were talking to a machine. This also gave rise to the famous Turing test. The goal of natural language processing is to allow that kind of interaction so that non-programmers can obtain useful information from computing systems. NLP is important technology in bridging the gap between human communication and digital data.

#### Why is this difficult for Computers?

We hardly face any difficulties in understanding a sentence in a language that we know and that's because we have a large knowledge base, mapping of words or sentences with our common sense knowledge of the world take place instantly inside our brain. We are easily able to derive meaning out of sentences by applying in our common sense knowledge along with our experience of similar situations even if there were a lot of ambiguities in the speech that we are hearing or the text that we are reading. This might sound funny in the beginning because this is very apparent to us and we may not be even aware about these processes occurring inside our brain because they happen with so ease but these our complex processes that scientists even with intensive research in this field have failed to understand in a way they would have loved to. And it is interesting to know that some of the difficulties that are there are because the natural language content contains a lot of ambiguities and that's because we omit a lot of common sense knowledge and keep a lot of ambiguities while we speak and that's because we assume that the receiver would be able to decipher it with his common sense knowledge and understanding of the context.

#### Let's take a conversation for example. (I have created this myself based on several examples that I remembered while writing this piece of text, it would be nice to get some feedback if anyone finds something wrong in this example)

**Mom**: It's raining today but the school is open.

**Son**: But I'm not feeling like going to school today.

**Mom**: Father will be angry if he comes to know about this.

**Son**: Ok I'm going to dress up.

For us, this converastion might be easy to understand but for computers this can be difficult. Let's analyse this.

The first line might appear crystal clear to us because of our common sense knowledge of the world and experience of similar situations but this is not the case for computers. "It's raining today". Okay. By this line we would instantly infer that it's raining outside the speaker's house and also in the area the kid's school is located and though it's raining, the school is open. But how does a computer understand this? How does it know where is it raining? What should it infer by raining **today**? What relationship does raining have with the school being open and why the people concerned are discussing the same? What does the word **open** mean here? We know that it means the school is working but how should the computer infer that since the word open has different meaning in different context.

In the third line what does the word 'Father' means? Does it mean the kid's father or father of the school. Why will the father be angry and at whom will he be angry? Also to infer the reason about the father's anger we need to go one or two sentences back. 

"Ok I'm going to dress up." What did the kid intend to say here? We understand that he means that he is getting ready for going to school but how does a computer understand that? Also we can have multiple interpretations in our mind at the same time for this sentence and can modify our thoughts or understanding and easily deal with the situation when one of our interpretations go wrong using some sort of feedback mechanism but how is the computer supposed to deal with such sort of ambiguous situation. Now you have clearly understood how difficult this can be but let's also see how this has been made easy by scientists doing immense research in the field of Computer Linguistics, NLP and Machine Learning and other related fields. I used the term 'easy' to symbolise the immense contributions in this field and there is a lot we have achieved but the state of art of NLP is a far from where we can feel satisfied and there is still a long way to go and this field even more interesting for carrying on a research.

  
#### Stages of Natural Language Processing

Natural language processing is broken down into roughly four stages:

**Morphological Processing**: The purpose of this stage of language processing is to break strings of language input into sets of tokens consisting of discrete words, sub-words and punctuation forms.

For example a word "unhappily" can be broken down into three sub-words tokens as:

un-happy-ly
 
**Syntax Analysis**: The purpose of syntax analysis is to check that a string of words is well formed and to break it up into a structure that allows the syntactic relationships between the different words.

For example the sentence  "The large cat chased the rat" after syntactic analysis would be de-structured as below:

![Syntax Analysis](../../assets/images/syntax-analysis.PNG)

**Semantic Analysis**: Semantic analysis deals with evaluating the meaning of the sentence. Let us consider the sentence " A dog is chasing a boy on the playground." We'll immediately map such a sentence with what we have in our knowledge base. For example we may imagine a dog and there is a boy and there's some activity going on there. For computers we need symbols to denote that say d1 for dog, b1 for boy and p1 for the playground. We can further infer some other things from this representation and we do the same while we read a text and this is called inference. For example using a rule like scared(d1,b1,p1) the computer may further infer that the boy is scared. 

**Pragmatic Analysis**: This is also called speech act analysis. This is used to understand the speech actor of a sentence. There's some intent behind what we speak. For example, one possible intent of a person behind saying this (" A dog is chasing a boy on the playground.") might be to remind another person to bring back the dog.


#### Ambiguities in Natural Language Processing

**Word-Level Ambiguity**: A word can have different syntactic categories for example **man** can be a noun or a verb. Also a verb might have several meanings. For example the word root might mean the root of a tree or a square root.

**Syntactic Ambiguities**: This arises because we can assign different syntactic structures to the same sequence of words. For example the sentence 'Natural Language Processing' can be interpreted in two ways. One could processing of natural language which is what is usually means and the other could be language processing is natural.

**PP Attachment Ambiguity**: This is called the prepositional phrase attachment ambiguity and again has to do with different syntactic structures that can be assigned with the same sequence of words. For example consider the sentence "A man saw a boy with the telescope". Now this can be interpreted in two ways, one could be that the man saw a boy using a telescope (telescope here is an instrument of seeing) and the other could be that the man saw a boy and the boy had a telescope with him. So depending upon the attachement point of prepositional phrases the meaning could differ and is generally resolves using knowledge of the context.

**Anaphora Resolution**: Consider the sentence "John persuaded Bill to buy a TV for himself". Now the question here is does himself refers to John or Bill? 

**Presuppostion**: Consider the sentence "He has quit smoking". This implies that the person smoked before. This may be very apparent to us but not for computers.

 
#### State of the Art of NLP

We can do part of speech tagging pretty well with 97% accuracy. We can do partial parsing pretty well too with 90% accuracy. This results are relative to the dataset and are based on the news dataset.

In terms of semantical analysis we are far from being able to do a complete understanding but we have techniques that can help us to gain partial understanding of the sentence.

**Entity Extraction**: This deals with extracting entities from a piece of text. Recognising people, location, organisation in a piece of text. 

**Relation Extraction**: This deals with extracting of relations in a piece of text. This person visited that place or this person is the CEO of this company. 

**Word-Sense Disintegration**: Using this we can figure out whether a word in a sentence would have certain meaning in one context and a different meaning in another context. It's not perfect though. They're not perfect. It works well for some entities and it's difficult in case of some.

**Sentiment Analysis**: Using sentiment analysis we can derive whether a sentence is positive or not. 

**Inference**: It's difficult to derive inference from a piece of text and we're not there yet in terms of inference. Also in terms of speech act analysis we're not there yet, we can do it for special cases in limited domains where there are a lot of restrictions but we can't do this reliably. 









