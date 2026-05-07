# Whisper to TextGrid Batch Processor

This repo contains an associated [Colab notebook](Whisper_to_TextGrid_Batch_Processor.ipynb). The notebook is designed to automate the transcription of large audio files, and convert the transcriptions to time-aligned SRTs TextGrids. It utilizes a Whisper model for speech recognition and the Silero Voice Activity Detector (VAD) for silence detection. This notebook is geared for linguists or language researchesr who want to transcribe audio files such as for an oral corpus. We utilize a Colab file so that we can use Google computing units instead of relying on personal GPUs. 

The workflow of the script is as follows:
1) It takes a folder of audio files as input.
2) It detects the silence intervals in an audio file, using Silero Voice Activity Detector (VAD). 
3) It breaks up the speech stream into separate non-silent chunks.
4) Each non-silent chunk passes through your transcription model to get transcribed
5) The individual chunk transcriptions are concatenated to create your final transcription
6) The output is saved as SRTs and TextGrids.

For step 4, you can plug in the repository name of a Whisper model from Hugging Face. Otherwise, if your model is not on Hugging Face or is not a Whisper model, you'll need to modify the code to set up the model in section 1.3

The only work you need to do is in section 1, where you enter your folder path, file names, and Whisper model information.

Note: I do not use speaker diarization. I have found that that the diarization results were often unreliable, and would lead to a lot of duplicate work in moving TextGrid intervals between tiers. But it can be a possible follow-up to automate this. The trick would be the determine the speaker of each non-silent interval, and then reassign these intervals across the tiers.
