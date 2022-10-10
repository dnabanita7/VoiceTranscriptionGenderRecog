# Gender Recognition using Voice
This repository is about building a deep learning model using TensorFlow 2 to recognize gender of a given speaker's audio and transcribe the audio with guessing percentage score. The commands only work on linux so far. I have not tested it on mac and other OS.

## Requirements
It is preferred to create a virtual environment so that dependencies don't clash with other packages.
For creating a virtual environment, you can type in the following commands in the terminal:

    python3 -m venv /path/to/new/virtual/environment
    source /virtual_path/bin/activate

Most of the dependencies are written in requirements.txt file but you need to have few more dependencies such as:

  sudo apt-get install libasound-dev portaudio19-dev libportaudio2 libportaudiocpp0 python3-pyaudio jackd2

Finally you can install the required libraries:

    pip3 install -r requirements.txt

## Dataset used

[Mozilla's Common Voice](https://www.kaggle.com/mozillaorg/common-voice) large dataset is used here, and some preprocessing has been performed.

If you wish to download the dataset and extract the features files (.npy files) on your own, [`preparation.py`](preparation.py) is the responsible script for that, once you unzip it, put `preparation.py` in the root directory of the dataset and run it.

This will take sometime to extract features from the audio files and generate new .csv files.

## Training
You can customize your model in [`utils.py`](utils.py) file under the `create_model()` function and then run:

    python train.py

## Testing

[`test.py`](test.py) is the code responsible for testing your audio files or your voice:

    python test.py --help

**Output:**

    usage: test.py [-h] [-f FILE]

    Gender recognition script, this will load the model you trained, and perform
    inference on a sample you provide (either using your voice or a file)

    optional arguments:
    -h, --help            show this help message and exit
    -f FILE, --file FILE  The path to the file, preferred to be in WAV format

- For instance, to get gender of the file `test-samples/27-124992-0002.wav`, you can:

      python test.py --file "test-samples/27-124992-0002.wav"

    **Output:**

      Result: male
      Probabilities:     Male: 96.36%    Female: 3.64%

  There are some audio samples in [test-samples](test-samples) folder for you to test with, it is grabbed from [LibriSpeech dataset](http://www.openslr.org/12).
- To make inference on your voice instead, you need to:

      python test.py

    Wait until you see `"Please say something.."` prompt and start talking, it will stop recording as long as you stop talking. Then it will show a prompt of `"Now recognizing.."` when the script tries to understand what the speaker says. After a short while, you will listen the audio output of the guessed transcription and see the audio percentage of confidence for the audio output.
