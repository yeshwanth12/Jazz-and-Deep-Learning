# Jazz-and-Deep-Learning
Generating Jazz music using an LSTM network

# Objective
You want to create a jazz music piece specially for your friend's birthday. However, you don't know to play any instruments or music composition. Fortunately, you know deep learning and can solve this problem using an LSTM network.
The network is trained to generate novel jazz solos in a style representative of a body of performed work.
<img src="images/jazz.jpg" style="width:450;height:300px;">

# Dataset
The model is trained on a corpus of [Jazz music](./data/30s_seq.mp3). Download it to listen to the sample data

The musical data is preproccessed to render it in terms of musical "values."
You can informally think of each "value" as a note, which comprises a pitch and duration. For example, if you press down a specific piano key for 0.5 seconds, then you have just played a note. In music theory, a "value" is actually more complicated than this--specifically, it also captures the information needed to play multiple notes at the same time. For example, when playing a music piece, you might press down two piano keys at the same time (playing multiple notes at the same time generates what's called a "chord"). 

# Model Overview
Here is the architecture of the model.
* The model is trained such that it predicts the next note in a style that is similar to the jazz music that it's trained on. The training is contained in the weights and biases of the model. 
* The weights and biases are used in a new model which predicts a series of notes, using the previous note to predict the next note. 
* The weights and biases are transferred to the new model using 'global shared layers'
<img src="images/music_generation.png" style="width:600;height:400px;">

* X = (x1, x2, ... , xT_x) is a window of size T_x scanned over the musical corpus. 
* Each xt is an index corresponding to a value.
* y^t is the prediction for the next value.

# Prediction and Sampling
<img src="images/music_gen.png" style="width:600;height:400px;">

At each step of sampling:
* Take as input the activation 'a' and cell state 'c' from the previous state of the LSTM.
* Forward propagate by one step.
* Get a new output activation as well as cell state. 
* The new activation 'a' can then be used to generate the output using the fully connected layer.

# Output
To listen to your music, go to [output](./output) and download "my_music.midi". Either play it on your computer with an application that can read midi files if you have one, or use one of the free online "MIDI to mp3" conversion tools to convert this to mp3.

# References

The ideas presented came primarily from three computational music papers cited below. The implementation here also took significant inspiration and used many components from Ji-Sung Kim's GitHub repository.

- Ji-Sung Kim, 2016, [deepjazz](https://github.com/jisungk/deepjazz)
- Jon Gillick, Kevin Tang and Robert Keller, 2009. [Learning Jazz Grammars](http://ai.stanford.edu/~kdtang/papers/smc09-jazzgrammar.pdf)
- Robert Keller and David Morrison, 2007, [A Grammatical Approach to Automatic Improvisation](http://smc07.uoa.gr/SMC07%20Proceedings/SMC07%20Paper%2055.pdf)
- François Pachet, 1999, [Surprising Harmonies](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.5.7473&rep=rep1&type=pdf)
- Sequence Models, Deep learning Specialization by Deeplearning.AI : https://www.coursera.org/learn/nlp-sequence-models
- 
