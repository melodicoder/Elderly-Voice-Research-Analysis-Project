# Elderly Voice Research Project

## Introduction and technical learning
<p>This is a research project a few of my peers and I conducted under the guidance of Professor Chen Jer-Ming from October 2021 to February 2022. The goal of the project was to develop a machine learning algorithm or a program that will take in a vocal sample of an elderly voice and detect whether the elderly suffers from cognitive disorders such as dementia. While it was not able to see the project to the end, it was still a valuable experience in improving my analysis skillset.</p>

## Technical Learning
<p>In the beginning weeks of the project, the professor gave a few lectures on the scientific terms behind the study of vocals. The team members also attended a workshop from the professor's colleague who is an expert in the field of vocal science on the technical procedures often used in audio classification. During this workshop, we were taught how to utilise the Librosa package in Python that is useful for manipulating and analysing auditory data. Professor Jer-Ming also gave a tutorial on how to use Adobe Audition, a software used to edit audio data.</p>

## Data Source
<p>The data, in other words the elderly audio samples, came from TTSH and are collected from elderlies living in undisclosed hospices and elderly homes and are collected from both healthy elderlies and elderlies diagnosed with dementia. All the samples are either in English or Chinese. Note that due to data privacy, the raw audio files will not be shown in this repository.</p>

## Data processing
<p>The simplest portion of a spoken word is called a **phoneme**. For instance, the phrase 'jumping bird' can be broken down into the phonemes '[j][ah][m][p][i][ng] [b][er][d]', with the content of each square bracket being one phoneme. Note that there is no international standardised set of phonemes so before we started parsing the data we came up with a set of phonemes that every member agree would sufficiently cover every possible sound in the English and Chinese language. The document on the list of phonemes that was developed for the project can be found in the Word document in this repository. 

The raw elderly audio samples is then manually transcribed into phonemes according to that developed set of phonemes as much as possible. Each raw audio clip from each sampled elderly is then also snipped into short audio clips of each instance of each phoneme in that clip manually. The phoneme audio clips from all the audio clips are then categorised into the different phonemes and whether the elderly speaking in that audio is known to be healthy or diagnosed with dementia. We then have a dataset of phoneme samples from healthy elderlies and another dataset of phoneme samples from elderlies with cognitive disorders for each particular phoneme. The amplitudes of the audio samples are increased during this data preprocessing so that we were able to identify the phonemes spoken as clearly as possible. It is to note that the phoneme transcription was solely based on the sounds spoken and neither the words that the elderly was perceived to say nor the context of the speech. A couple of samples of the transcriptions are in the Excel files in this repository.</p>

## Data analysis
<p>The main bulk of the project is finding a good method to extract meaningful insights from the phoneme audio clips. During this stage, each member was given the freedom to come up with their own method of data analysis after which each of us presented our ideas.

Before explaining my method, there is a need to explain the main features of an audio clip of a speech. A piece of audio is a signal and audio signals can be considered as a power spectrum which simply covers the intensity of a signal over the duration of the signal. This power spectrum can be represented by a mel-frequency cepstrum (MFC). A cepstrum is a mathematical transformation that analyses the spectrum. There is another technical term audio researchers use called **mel-frequency cepstral coefficient (MFCC)** that simply put are the coefficients of the MFC which represents the spectral shape of the sound signal.

After more data preprocessing, it was found that a phoneme audio clip always contains 13 MFCCs. The method I initially considered included having the machine learning algorithm eventually compare the mean MFCCs across all the clips of a particular phoneme from healthy elderlies and the mean MFCCs across all the clips of a particular phoneme from elderlies with dementia.

With that in mind, the MFCC from each phoneme audio clip is extracted using the ```librosa.feature.mfcc``` function in Librosa. A heatmap of the MFCCs of each phoneme audio clip is plotted using Matplotlib.</p>

![Heatmap of an 'l' phoneme from a healthy elderly](/Screenshot%202024-10-27%20231107.png)
<p style="text-align:center;">The heatmap of an 'l' phoneme from a healthy elderly</p>

<p>The bar charts and trendlines of the mean of each of the 13 MFCCs across all healthy elderly clips and the mean of each of the 13 MFCCs across all clips from elderly with dementia on the same plot. The full code for two such comparisons are in the IPython notebooks attached. All the analysis is again in the attached IPython notebooks.</p>

![Bar charts and trendlines of mean of first 6 MFCCs of 'l' phoneme collected from healthy elderlies (blue) and elderlies with dementia (red)](/Screenshot%202024-10-27%20231128.png)
<p style="text-align:center;">Bar charts and trendlines of mean of first 6 MFCCs of 'l' phoneme collected from healthy elderlies (blue) and elderlies with dementia (red)</p>
