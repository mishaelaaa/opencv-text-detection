# OpenCV Text Detection

[![Build Status](https://travis-ci.com/mishaelaaa/opencv-text-detection.svg?token=wspsaqLEAFcDhxFbHWvQ&branch=master)](https://travis-ci.com/mishaelaaa/opencv-text-detection)

These are my first attempts at recognizing text. I've borrowed from [Adrian Rosebrock](https://www.pyimagesearch.com/author/adrian/). 
The project has two directions: recognition of text from an image or from a video.
  - *[image](https://github.com/mishaelaaa/opencv-text-detection/blob/master/opencv-text-detection/text_detection.py)*
  - *[video](https://github.com/mishaelaaa/opencv-text-detection/blob/master/opencv-text-detection/text_detection_video.py)*
  
# SVHN dataset

The Street View House Numbers dataset contains 73257 digits for training, 26032 digits for testing, and 531131 additional as extra training data. The dataset includes 10 labels which are the digits 0-9. The dataset differs from MNIST since SVHN has images of house numbers with the house numbers against varying backgrounds. The dataset has bounding boxes around each digit instead of having several images of digits like in MNIST.

# Scene Text dataset
This dataset consists of 3000 images in different settings (indoor and outdoor) and lighting conditions (shadow, light and night),  with text in Korean and English. Some images also contain digits.

# Devanagri Character dataset
This dataset provides us with 1800 samples from 36 character classes obtained by 25 different native writers in the devanagri script.

### Natural scene text detection is different though — and much more challenging.

Due to the proliferation of cheap digital cameras, and not to mention the fact that nearly every smartphone now has a camera, we need to be highly concerned with the conditions the image was captured under — and furthermore, what assumptions we can and cannot make. I’ve included a summarized version of the natural scene text detection challenges described by Celine Mancas-Thillou and Bernard Gosselin in their excellent 2017 paper, Natural Scene Text Understanding below:

* **Image/sensor noise**: Sensor noise from a handheld camera is typically higher than that of a traditional scanner. Additionally, low-priced cameras will typically interpolate the pixels of raw sensors to produce real colors.
* **Viewing angles**: Natural scene text can naturally have viewing angles that are not parallel to the text, making the text harder to recognize.
* **Blurring**: Uncontrolled environments tend to have blur, especially if the end user is utilizing a smartphone that does not have some form of stabilization.
* **Lighting conditions**: We cannot make any assumptions regarding our lighting conditions in natural scene images. It may be near dark, the flash on the camera may be on, or the sun may be shining brightly, saturating the entire image.
* **Resolution**: Not all cameras are created equal — we may be dealing with cameras with sub-par resolution.
* **Non-paper objects**: Most, but not all, paper is not reflective (at least in context of paper you are trying to scan). Text in natural scenes may be reflective, including logos, signs, etc.
* **Non-planar objects**: Consider what happens when you wrap text around a bottle — the text on the surface becomes distorted and deformed. While humans may still be able to easily “detect” and read the text, our algorithms will struggle. We need to be able to handle such use cases.
* **Unknown layout**: We cannot use any a priori information to give our algorithms “clues” as to where the text resides.

#  EAST deep learning text detector
![The structure of the EAST text detection Fully-Convolutional Network][image]

[image]: https://github.com/mishaelaaa/opencv-text-detection/blob/master/opencv-text-detection/images/readme/opencv_text_detection_east.jpg "opencv text detection east" 

# CRNN
Convolutional Recurrent Neural Network (CRNN) is a combination of CNN, RNN, and CTC(Connectionist Temporal Classification) loss for image-based sequence recognition tasks, such as scene text recognition and OCR. 
![CRNN : ][image1]

[image1]: https://github.com/mishaelaaa/opencv-text-detection/blob/master/opencv-text-detection/images/readme/CRNN.png "CRNN" 

# Tesseract
So, what is the OCR? Optical Character Recognition. In other words, OCR systems transform a two-dimensional image of text, that could contain machine printed or handwritten text from its image representation into machine-readable text. OCR as a process generally consists of several sub-processes to perform as accurately as possible. The subprocesses are:

* Preprocessing of the Image
* Text Localization
* Character Segmentation
* Character Recognition
* Post Processing

The sub-processes in the list above of course can differ, but these are roughly steps needed to approach automatic character recognition. In OCR software, it’s main aim to identify and capture all the unique words using different languages from written text characters. Some of the models are:

* Tesseract OCR Features
* Preprocessing for OCR using OpenCV
* Running Tesseract with CLI and Python
* Limitations of Tesseract engine


> **Tesseract OCR**

Tesseract is an open source text recognition (OCR) Engine, available under the Apache 2.0 license. It can be used directly, or (for programmers) using an API to extract printed text from images. It supports a wide variety of languages. Tesseract doesn't have a built-in GUI, but there are several available from the 3rdParty page. It can be used with the existing layout analysis to recognize text within a large document, or it can be used in conjunction with an external text detector to recognize text from an image of a single text line.

![OCR Process Flow to build API with Tesseract][image3]

[image3]: https://github.com/mishaelaaa/opencv-text-detection/blob/master/opencv-text-detection/images/readme/ocr_flow.png

> **Technology - How it works**

LSTMs are great at learning sequences but slow down a lot when the number of states is too large. There are empirical results that suggest it is better to ask an LSTM to learn a long sequence than a short sequence of many classes. Tesseract developed from OCRopus model in Python which was a fork of a LSMT in C++, called CLSTM. CLSTM is an implementation of the LSTM recurrent neural network model in C++, using the Eigen library for numerical computations.


![Tesseract 3 OCR process from paper][image4]

[image4]: https://github.com/mishaelaaa/opencv-text-detection/blob/master/opencv-text-detection/images/readme/How_it_works.png

