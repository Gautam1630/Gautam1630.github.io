---
layout: post
title: Reading Comprehension using Entity-based Memory Networks
---
Draft : Shubham and Harsh 



“ As I entered the room I saw there was a green apple kept on the table.….”

As you were reading this sentence  somewhere down the line you started imagining yourself entering a room and looking at a green apple kept on a table, you did not really remember the sentence and the words yet somewhere down the line you created an imaginary ‘existence’ of whatever was happening!  

Memory networks as we saw in our previous post did something inline to this, however they remember stuff as vectors which are formed out of sentences. Often it is difficult to explore the information contained in the text specially in case of long  and complicated sentences. How often have you said “In essence the paragraph says….!” Can we train a network to do something analogous to that?    


figure from the paper...

In our previous blog we saw that how deep learning can be used very effectively for training memory networks which could be used for answering questions based on some given information. The experimental setup included several tasks….. *please elaborate a bit….*

Just to recapitulate the memory network has 4 main modules:

I: Input module.
G: Generalization module 
O: Output feature module. 
R: Response module. 

If you feel you wanna read memory networks again you can read this post. (put the link here to Deeksha Blog on memory networks!) 

Let’s see how can we implement such a learning model to capture entities. 

* Let’s take up an example from the paper itself to understand the idea clearly. Will try to summarise the overview wala example. It’s very long and tough.. we might just refer it here in case nahi hua toh* 

Entity based Memory Network: Model Overview

As you can see in the figure we consider each sentence one by one. There are some extracted entities and the new sentence. Both of them are used to create what is referred to as the state of the entities. Now based on the question, some information from the entity is focussed upon and used for generating the output feature which is further converted into the appropriate response.  

Let’s look at the working of each module in detail:

I: Input module: This module converts the sentences into a vector.  The module takes as  an input a sentence and converts it into a vector. Meanwhile, it also extracts all the entities it contains. The paper assumes that we have the entities annotated for each sentence. The question is also processed using this module. The authors of the paper used an autoencoder to convert the sentence into a vector representation.

Generalisation Module: Every time as you are looking at new sentences there are two possible choices .
you might get some information about the existing entities 
or you might catch hold of some new entities itself.

The update in entities takes place using the generalisation module. The figure schematically shows how the module works. 



For entities that are not contained in the memory pool, the model would create a new memory slot for them and initialize these slots using pre-learned word embedding.

If it looks at new information about the present entities, it needs to update their state. How can that be done? The model asks us to construct the sentence solely from its entities. So we define a function f2 which will take one by one the entities of sentence as input and output the sentence vector (S2). The f2 model is trained by comparing the output (S2) with S and minimizing the loss using stochastic gradient descent it is trained.


In the implementation a Gated Recurrent Unit (GRU) is used as f2 which update the sentence by taking entities as input and then entities are updated by comparing S1 and S2. This way we make sure entity contains sufficient context and information regarding the sentences being read.

3. O: Output feature module. the output module is triggered whenever the model stumbles upon a question. It retrieves the related entities according to the question asked and retrieves the output feature. 
It is triggered whenever a question arrives. Retrieve related entities according to the input question and then produce an output feature vector accordingly.


 Whenever a question arrive its vector q is created l and a new vector Q is initialised as Q  and iterated over all entities in memory pool and updated alongside through GRU, in jth iteration(when jth entity occur)  probability (or score p) of ek being selected to compose the feature vector for answering q is calculated. p  is calculated by GRU of previous Q state and ek and then taking sigmoid of it, now maxima of p (call it E) is used to update output feature O along with e (entity) (we have used GRU here).  



4. R: Response module. Generate the response according to the output feature vector.
To generate the final answer, we use a simple neural network which takes the feature vector O as input and predict a word as output. 
p = v(O) = softmax(tanh(W ∗ O + b)). The word with the highest probability is selected.
 

Need for Deep Learning
*End to end lstm wala blog main yeh daalenge and we will refer to it over here*
Features such as bag-of-words, token frequencies and so on are unable to capture the rich information in text. Often outside knowledge is required towards better performances. Traditional approaches heavily rely on rules or structured knowledge. Construction of structured knowledge is both time and money consuming. Secondly it is a huge challenge to models flexible and powerful enough to learn to employ these information extracted. Thus the progress of using machine learning for QA has been slow.
Deep neural networks represent all the features of a sentence using vectors which is a unified representational form for all the necessary information. Outside knowledge learnt from large corpus can be encoded into word vectors. Information obtained locally is also represented using vectors. Deep neural network models with many layers are designed to fuse information obtained from different sources
Memory Networks
The key of memory network is to store all historical sentences in a memory pool. The model is trained to look for related sentences when a question comes. Then based on the related sentences, an answer is predicted for the question. Memory network remembers all sentences it has read so that it can look for useful ones when facing questions
Memory Networks: The model
The memory network contains four parts: the input module which converts sentences into vectors, the memory which keeps all sentence vectors a retrieval module and a response module. Whenever a question comes, the question is turned into a vector and the question vector is used to retrieve the memory for related sentences. The 3 response module is used to predict an answer based on the related sentences. The core component is the memory pool that stores all the input sentences so that they can be retrieved later to answer questions. This model contains several neural networks which are jointly optimized according to the task.




