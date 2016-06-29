# Plan for Research
## I. Data

### 1. Online (On) and Offline (Off) patterns

### 2. Languages/Types
#### A. English
+ IAM DB (lines, words,...)
+ IAM OnDB (lines, words,...)
+ IBM UB1 (Online + Offline) [query & form]
+ Unipen (Online)

#### B. Japanese
+ Nakayoshi Kuchibue (Online) (characters)
+ Kondate (Online) (strings)
+ XXX (Offline)

#### C. Vietnamese
+ VnOnDB (Online) (strings)

#### D. Mathematics
+ CROHME (Online)
+ MathBrush (Online)
+ MNIST (Offline)
+ SVHN (Offline)

#### E. Non-text/Text
+ Kondate (Online)
+ IAM Mondo (Online)

## Tasks
+ Classification (1-to-1)
+ Image Recognition/Classification
+ Sequence Classification
+ Sequence to Sequence
  + Encoding/Decoding
  + Sequence Transcription
+ Structure parsing (recursive network)
+ Retrieval information (ink search)

## II. Problems
### 1. Generating data
#### Offline data from online patterns
+ Draw Bitmap (stroke's width problem)
+ Blurring

#### Generating artificial patterns (both)
+ Online: resampling, sigma-lognormal method, affine transform
+ Offline: transformations

### 2. Features extraction & normalization/standardization (both)
+ Online: point-based features (4 basics+8extends), context map, shape context
+ Offline:
  + Gradient features
  + Alvaro thesis, offline features for MathExp
  + Conv layers for extracting features

### 3. Segmentation (line/word) (both)
+ Online: off-stroke feature, clustering, linear regression
+ Offline: Sliding windows + RNN

### 4. Offline character region detection (both)
+ Faster-R-CNN, R-FCN (best) [GPU based, caffe, matlab interface]

### 5. Recognition (BLSTMs & CNNs)
+ Recoding LSTM & CNN (Done)

  #### Multi-networks/multi-recognizers combination
  + Ensemble method

  #### Transcription (CTC)
  + Recoding

### 6. Decoding
  - Lexicon-free
    + Prefix search decode
    + Reduce waiting time of prefix search   
  - Lexicon-driven
    + FST lexicon
    + Language model integration
      + Tri-gram using CMU-Cam toolkit
      + RNN based
      + Perplexity

### 7. Mathematic Expression parsing
+ Recursive neural networks (ME formula training and parsing)

### 8. Ink search by lattice/keyword spotting
+ LSTM method
+ Lattice search

### 9. Deep Learning frameworks and GPU accelerating
+ Theano (python interface + CUDA kernel)
+ cuDNN library (C++ interface)
