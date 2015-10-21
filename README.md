# Comprehensive OCR System for Telugu Language
## The Banti Framework

This framework relies on the ability of a segmentation algorithm to break the
text in to glyphs. Hence it can be extended to other scripts with well 
seperated images like Malayalam, Oriya, Tamil, Kannada, Thai etc.

# Features
+ Opens box files generated by banti (segmentation program)
+ Passes them to a neural network trained by [theanet](https://github.com/rakeshvar/theanet)
+ n-gram modelling of the language
+ Ability to stich broken glyphs (using the language model).

# Dependencies
1. Python3
1. Numpy, Scipy, Nose etc.
1. [Theano](https://github.com/Theano/Theano)
1. [banti segmenter](https://github.com/rakeshvar/banti)
1. [Theanet](https://github.com/rakeshvar/theanet)

# Installation Instructions

1. Install python3

  You might already have it. Just type ```which python3``` and  check. Make sure you also have ```pip3```. Python3.4 comes with ```pip3```. Python3.3 and older need additional installation of ```pip3```.

2. Install ```Theano``` after installing its dependencies. Here are the [General](http://deeplearning.net/software/theano/install.html) and  the 
[Ubuntu-specific](http://deeplearning.net/software/theano/install_ubuntu.html#install-ubuntu) instructions. You just need to install numpy, scipy, nose etc.

3. Install [Theanet](https://github.com/rakeshvar/theanet) by running the setup.py

4. Clone this repo. ([telugu_ocr_banti](https://github.com/rakeshvar/telugu_ocr_banti))

5. Set the following theano flag(s). I just put the following in my .bashrc file.
  ```sh
  export THEANO_FLAGS='floatX=float32'
  ```

6. Get the required files to load the neural network and the ngram library.
  ```sh
  # change to cloned project directory
  mkdir library
  wget http://stanford.edu/~rakesha/banti/library/4hidaux_252611_01.pkl -O library/nn.pkl
  wget http://stanford.edu/~rakesha/banti/library/mega.123.pkl -P library/
  ```

7. Run the ocr program 
  ```sh
  python3 recognize.py sample_images/praasa.box 
  # Run for help
  python3 recognize.py -h
  ```
  Here you are running on the provided sample image ```praasa.box``` genereated from ```praasa.tif``` (both in the ```sample_images``` directory)

8. OCRing your own images.
  ```sh
  python3 recognize.py sample_images/praasa.tif
  ```

  Note that `recognize.py` needs images in `.box` format. These 
  files are genereated by [banti segmenter](https://github.com/rakeshvar/banti). 
  You can install it to genereate box files from your tiff files. Once you 
  obtain the `banti_segmenter` binary/executable. You can leave that in the 
  same directory as `recognize.py` or you can pass it as an argument.
  This will enable `recognize.py` to convert tiff files to box files.
  
  Alternatively to get box files, you can try to run [this binary]
  (https://stanford.edu/~rakesha/banti/banti_segmenter) that has been built on a 64-bit linux ubuntu machine. (Run it without any arguments to see all options.) 
