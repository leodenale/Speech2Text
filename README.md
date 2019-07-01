# Speech2Text
Speech to Text - Running in your browser using Google Colab

Reference Article: https://medium.com/datadriveninvestor/speech-to-text-app-in-your-browser-using-deep-learning-35889fbd50ed

# Speech to text app in your browser using deep learning

## Introduction
Deep speech is an automatic speech recognition technique using deep learning. Modern Era of speech recognition started in 1971 when Carnegie Mellon University started a consolidated research effort (ref: CMU’s Harpy Project) to recognize over 1000 words in human speech. In 2011, application of speech recognition in mobile devices was pioneered by Google with their voice search app. Soon, voice assistants like Siri, Alexa, Cortana and Google captured the excitement.

These modern day devices employ variety of systems including a DSP for processing on the raw speech signal like frequency domain conversion, restoring only the required information etc. This signal is then translated to intermediate phonetic representation, which is compared with the reference speech pattern to determine the actual words or the pattern of words.

End-to-end speech recognition system eliminate the need for phonetic conversion. Such a system directly transcribes audio spectrograms with character sequences directly to words. In this article, we use [“Deep Speech”](https://arxiv.org/abs/1412.5567) — a deep learning network model.

## Deep Learning
LSTM Recurrent Neural Networks (RNNs) and Time Delay Neural Networks (TDNN) have proven promising in improving quality of speech recognition. Their inferencing performance, however, needs improvement. Deep speech uses simplified form of RNN as shown in the picture below:


Deep Speech: Scaling up end-to-end speech recognition

## Speech to text in the browser
So what does it take to develop a MP3 to text translator using deep speech? For the speech input we choose MP3 format, since MP3 enjoys the status of a standard technology and format for compressing a sound sequence into a very small file without losing quality significantly. So we use MP3 as input and use deep learning model “deep speech” for inferencing spoken words.

## App details
Deep speech model takes wav format as input. We use ffmpeg package in colab to convert mp3 input to wav format required for deep speech model with audio channels reduced to 1 and sampling frequency adapted to 16000. Audio code pcm_s16le is used to write raw PCM audio into a WAV container.
```
  !ffmpeg -i speech.mp3 -vn -acodec pcm_s16le -ac 1 -ar 16000 -f wav speech.wav
```
Next step is to load deep speech model with following parameters.
```
  # 1. Number of MFCC features to use
  N_FEATURES = 26
  # 2. Size of the context window used for producing timesteps in the input vector
  N_CONTEXT = 9
  # 3. Beam width used in the CTC decoder when building candidate transcriptions
  BEAM_WIDTH = 500
```

Once the base deep speech model is loaded, language model of choice (English, Mandarin, Hindi, German etc.) is loaded to inference. You are ready to upload mp3 file see magic in action.

## Notebook
Here is link to [google colab notebook](https://colab.research.google.com/drive/1fXJ_YUWACs0w8ohORFijuWo4_pCLMIEK) to download and play around for your speech and see if deep speech can recognize your words. Here is a snapshot of how to run your application in the cloud.

## Results
Deep speech heavily relies on the language model and works well on small sentences. It sometimes minces or joins spoken words.

References
- Deep Speech’s documentation - https://deepspeech.readthedocs.io/en/latest/index.html
- Machcine Intelligence in Design Automation - http://amzn.to/2paZ53b
- FFMPG — the multimedia framework - https://www.ffmpeg.org/documentation.html


