Spectro ID.

# Spectro ID
![spectro](https://user-images.githubusercontent.com/63719942/80239864-39ecee80-8661-11ea-9afa-a151a5b4cdc3.gif)
## Introduction
Sprctro ID is an application that allows you to play with music and emotions. Composed of two phases, it tries to play your mood according to the emotion you are showing. Then once you take a snapshoot, it reconstructs your face through a spectrogram. As a project for Advanced Coding Tools and Methodologies course of Master's Degree in Music and Acoustics Engineering at Politecnico di Milano, Spectro Id is an experiment that shows how your face might sound. Our source of inspiration was the Aphex Twin's spectrogram since he has made a great contribution to contemporary Electronic and Ambient Music.
## Tools 

### CLMtackr
In order to detect emotions we used CLMtrackr, which is a javascript library for fitting a facial model to faces in images or video, by using WebGL rendering. The facial model consists of 70 points. The CLMtrackr's algorithm fits the facial model by using 70small classifiers, one for each point in the model. Given an initial approximate position, the classifiers search a small region around each point for a better fit, gradually converging on the optimal fit.



![Schermata 2020-04-24 alle 18 58 15](https://user-images.githubusercontent.com/63719942/80240965-08752280-8663-11ea-83bd-e5a755865fe9.png)




Principal Component Analysis is used to build a model. It extracts the variations of the faces as linear combinations of vectors, or components. The first components that PCA extracts will usually cover basic variations from posture, such as yaw, pitch, followed by opening and closing mouth, smile, etc. Moreover, any facial poses can then be modelled as the mean points plus weighted combinations of these components, and the weight can be thought of as a parameter for the facial model. 



![Schermata 2020-04-21 alle 20 09 03](https://user-images.githubusercontent.com/63719942/79898718-05ccc000-840c-11ea-9005-8a17987858bd.png)



## Emotion Detection
Through a mean on the parameters of the facial model and comparing them with the data from a MUCT database, the library allows us to get four values, each one associated to a particular emotion. This process permits to manage the transitions of the visual and the sound contributions.


The face deforming filters are made by extracting the face and modifying its components according to the emotion array. Using the *dat.gui.js* we have created some controls hidden to the user which modify the data of the component all in once. In order to make the copy-paste operation natural, we have to use a method called *Poisson Blending* since the edges after the modification may not match the background. In addition, the chart bars give a real-time feedback and represent the actual values of each emotion by using *D3* library particularly suited for these tasks.

## Emotion Sound

In Spectro ID CLMtrackr is used to detect four emotions such as *Happiness, Sadness, Wander and Anger* and each emotion is associated to a random sound pattern. Our goal has been to define these patterns in such a way as to represent the mood related to the recognized emotion

### Musical Theory

The experience is based on some general rules of music theory. According to Wester Musical Culture, *Major* and *Minor Chords* have been chosen to describe the mood associated to Happy and Sad emotions respectively as well as *Augmented* and *Diminished Chords* are related to Surprise and Angry moods. Then the patterns are driven by a *Musical Scales* such as *Major* and *Minor Scale* or by some *Modal Scales* like *Dorian* or *Aeolian*. The synths do not play every note of that scale and the scales are extended to some octaves. Moreover, every time an emotion is recognized, the patters randomly choose the *First*, the *Second* or the *Third Inversion Chord* inside the scale to make the experience more dynamic and less repetitive and monotonous while the key of chord changes periodically according to the mood that is being represented.

### Sound Design

As the logo suggests, the musical theme is based on Electronic Music. 
In Spectro ID several synths are related to a single pattern by using Tone.js. It is a framework for creating interactive music in the browser. It provides synths, effects, and intuitive musical abstractions built on top of the Web Audio API. The latter has advanced, sample accurate scheduling capabilities and it has the AudioContext time, which is the reference clock that Web Audio uses to schedule events.

Every Emotion is enhanced by different presets and effect chains which are automated in order to give smooth transitions between recognized emotions.

## Spectrogram
The aim of the second phase is to create a sound identity starting from a photo as the hidden face in the spectrogram of the track *Equation* by *Aphex Twin*. 


![Schermata 2020-04-22 alle 19 11 58](https://user-images.githubusercontent.com/63719942/80012194-388abd00-84cd-11ea-9d1f-41c654ab9551.png)


A spectrogram is a visual representation of the spectrum of the frequencies of a signal as it varies with time with the amplitude of each frequency visualized as a grayscale value. Spectrograms are used extensively in the fields of music, linguistics, sonar, radar, and speech processing, seismology, and others. 
The common format is a graph with two geometric dimensions: one axis represents time and the other axis represents frequency from the bottom to the top.  A third dimension indicating the amplitude of a particular frequency at a particular time is represented by the intensity or color of each point in the image.

### Constructing sound face
The starting point is that an image is made by pixels. Each pixel raw of this image represents a sinusoid at a certain frequency. It means that the height of the raw, starting from the bottom, sets the pitch. The second dimension of the spectrogram is the width associated to the columns of the image and each column represents time fraction of the total time. 
The greyscale intensity of each pixel determines the amplitude (volume) of each sinusoid. A black pixel on the bottom row means "turn off the 5000 Hz tone", whereas a white pixel means "blast a 5000 Hz tone at max volume".

Relying on this idea, the aim was to extract different features (shades, edges, etc.) by means of several filters in order to obtain different data layers. Each layer can be thought as a score which will be played by a synth. The overlap of the synthesizer outputs, analyzed by a spectrogram, forms the sonic counterpart of the image. For this version of Spectro ID, only an edges detection filter is implemented in order to minimize the acquired data since the data managing is not already optimized.

The output of the filter is a matrix pixels. After a conversion, the matrix data are ready to be played. In particular they are divided in order to form some frequency bands and each of these bands is sent to a synthesizer. 
The simultaneous play of several synths forms the resulting spectrogram and creates dynamic and complex sound since the synthesizers may cover the entire audio bandwidth.

### Here below the links about the Demo and the application itself

https://www.youtube.com/watch?v=VtclPdXcr4Q&feature=youtu.be&fbclid=IwAR2tocxsNlFDJn6cqC6mFlzKy0_D7sXu3lyCTNbhJ45baZAizF6uKleAWBY


https://devkuvia.github.io/SpecrtoID/





