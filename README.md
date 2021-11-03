# Neural-Machine-Translation

1.Machine translation in a broad spectrum can be seen as translation of a sequence of words from one language to another preserving the meaning.

2.The objective of this project is achieved by using a special type of Recurrent neural network called LSTM having ability of learning long-term dependencies, which has a wide application speech processing.

3.We use an architecture called Seq to Seq modelling for achieving this objective of ours.

4.Here's how LSTMs work: 

img-1

    => Step-1: Decide how much of the past it should remember.
       img-2

    => Step-2: Decides how much this unit adds to the current state.
       img-3

    => Step-3 Decide what part of the current cell state makes it to the output.
       img-4

5.Seq to Seq model: 

img-5

    => Encoder: No outputs because we are not making any predictions.
                Only keep final state ht.
    => Decoder: the output of the encoder is given as an I/p to the decoder and subsequent chain is formed   
                for the rest of the network.  

        img-6

6.About the dataset that we used to train our machine: 

    => We use a file translations-dataset.txt file for our dataset.
    => On each line the text file contains an English sentence and its Spanish translation, separated by a 
       tab.
    => The file contains close to 10,000 samples or we can say translations from English to Spanish in the 
       above mentioned format.

7.We use the tokenizer provided by keras to tokenize the input, this needs to be done bcause our deep learning and machine learning models can work only on numbers.
    => From our dataset we get 2337 unique input tokens.
    => and 6316 unique output tokens. 

8.Word embeddings: 
    => Broadly speaking it means converting words into its corresponding multi dimensional vector 
       repesentation so that words with same/similar meaning have a similar representation.     
    => Just an output for the word "ILL"

    img-7
    
9.Creating the model: 
    => The first thing whici is done is to define our outputs.
    => We create an empty output array.
    => To make predictions, the final layer of the model will be a dense layer.
    => Therefore I need one hot encoded vectors as outputs. Since we use softmax activation function at the 
       dense layer.
    => So, we assign 1 to the column that corresponds to the integer representation of the word.
    => For instance, the integer representation for  "<sos> je suis malade" is
       [ 2 3 6 188 0 0 0 0 0 0 0 ]. 
    => In the output array, in the second column of the first row, 1 will be inserted. Similarly, at the 
       third index of the second row, another 1 will be inserted, and so on. 
    => Next we create 3 most important aspects of the project as follows: 
    => First one is encoder input placeholder.
    => Second one is decoder input placeholder.
    => Third one is the decoder dense layer dense layer.
    => The above mentioned layers are required in creating the model.

10.Finally we fit() the model to our dataset and the training begins.

11.This is an example to illustrate what happens during predictions:

    Step 1:
    I'm ill -> Encoder -> enc(h1,c1) 
    enc(h1,c1) + <sos> -> Decoder -> y1(je) + dec(h1,c1) 
    Step 2: 
    enc(h1,c1) + y1 -> Decoder -> y2(suis) + dec(h2,c2) 
    Step 3: 
    enc(h2,c2) + y2 -> Decoder -> y3(malade.) + dec(h3,c3) 
    Step 4: 
    enc(h3,c3) + y3 -> Decoder -> y4(<eos>) + dec(h4,c4)

The model will accept an input-padded sequence English sentence (in the integer form) and will return the translated Spanish sentence. 

12. Limitations: 

    => Neural machine translation is a fairly advance application of natural language processing and 
       involves a very complex architecture.
    => The seq2seq architecture is pretty successful when it comes to mapping input relations to output. 
    => However, there is one limitation to a seq2seq architecture.
    => The seq2seq architecture explained in this article is not capable of capturing context. 
    => It simply learns to map standalone inputs to a standalone outputs. 
    => Real-time conversations are based on context and the dialogues between two or more users are based on 
       whatever was said in the past. 

Therefore, a simple encoder-decoder-based seq2seq model should not be used if you want to create a fairly advanced chatbot.