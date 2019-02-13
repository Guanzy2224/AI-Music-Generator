# AI Music Generator

Multi-layer Recurrent Neural Networks (LSTM, RNN) for character-level language models in Python using Tensorflow.

Inspired from [sherjilozair's project](https://github.com/sherjilozair/char-rnn-tensorflow) which is inspired from [Andrej Karpathy's char-rnn](https://github.com/karpathy/char-rnn). Though those projects is designed to imitate text generation.

## Requirement

- Tensorflow 1.0

- Any Python version that support Tensorflow (Python3.7 does not yet)

## Datasets

- Data Input could be any form of music notation that is clean and easy to understand by AI. In this project, ABC notation is used because its high level integration reduces the minimum amount of data needed to train a working model.

- Tons of ABC notation data could be access at [abcnotation.com](http://abcnotation.com/)

## File Structure

- data: the folder holds input data that is stored in `input.txt`
- save: the folder holds periodically saved model during training process, these file will be load in sampling process or further training
- logs: logs for tensorboard
- sample music: sample input and sample output, in the format of both machine readable text and human listenable music

## Usage

- To train with default parameters on the tinyshakespeare corpus, run `python train.py`, or `python2.7 train.py`, `python3.6 train.py`, more specifically, `python train.py --data_dir=./data/nottingham/`. To access all the parameters use `python train.py --help`.

- To sample from a checkpointed model, `python sample.py`. The default sampling plan will generate string with 500 characters, to change that `python sample.py -n 5000` 5000 could be any reasonable positive integer number.

- To continue training after interruption or to run on more epochs, `python train.py --init_from=save`.

## Features and Improvements

- Ability to mimic human music composing pattern, knows how to repeat, modify, envolve and end

- One way to enhance the performance of AI is to feed in higher quality data. This can be done by
  1. Remove unnessary notes that come with oringinal data
  2. Delete songs with special music element
  3. Try to keep the structure as simple as possible
  
- AI tends to generate music with same structure as the input ones, which means it will have about same level of length. To make it generate longer melody than sample fed in, I changed the smapling method so that it will regenerate some sentence if that one leads the sequence to an inevitable end.

- Sampling from probability distribution will have a small chance of generating a disordant note in each step, but will almost certainly generate some bad piece if the sequence goes long enough. To avoid this, a probability threshold is set so that bad note will not appear as long as AI predicts it correctly.

## Youtube Video

- [A longer one generated by modified sampling method](https://www.youtube.com/watch?v=PccjWfVRXXg)

- [A shoter one generated by original sampling method](https://www.youtube.com/watch?v=fNOt6yYL1PA&t=21s)
