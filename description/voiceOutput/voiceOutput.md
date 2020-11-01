## 1. 사용한 모델

초기에 음성 변환을 위하여 사용한 모델은 cycleGAN을 이용한 감정변조였다. (참고:  [Emotional Voice Conversion and/or Speaker Identity Conversion with Non-Parallel Training Data](https://github.com/KunZhou9646/emotional-voice-conversion-with-CycleGAN-and-CWT-for-Spectrum-and-F0) ) 기존의 음성 변환 모델은 서로 다른 emotional pattern을 학습하기 위하여 parallel한 data set을 넣어주어야 했는데, 해당 모델은 parallel data가 없더라 할지라도 각 domain의 차이를 이용해서 감정을 학습하는 형식이다. 이를 진행할 때 음성정보 .wav 를 melspectogram형식으로 변환하여 해당 데이터를 서로 다른 GAN을 이용해 학습시킨 후 다시 처음의 음성으로 재합성하여 결과를 확인하였다. 

## 2. 왜 문제가 생겼는가?

다른 감정의 음성을 학습하여 그 감정정보를 빼주는게 아니라 두 domain의 차이점이 감정정보밖에 없었기 때문에 학습을 잘 진행할 수 있었던 것이었다. 즉 내가 다른 화자의 목소리를 넣거나, 기존에 학습한 데이터가 아닌 다른 content 를 주입할 경우 test 가 제대로 이루어지지 않는 모습을 확인할 수 있었다. 따라서 우리가 원하는 결과를 내기에는 부족하다고 판단하여 다른 모델을 찾기 시작했다. 

## 3. 왜 SpeechSplit 인가?

SpeechSplit 은 기존의 모델이 사용한 end-to-end 방식이 아닌 각각의 정보를 직접 분해하여 다시 재조합하는 과정을 거치기 때문에, 목소리에서 pitch 정보만 분리하여 내어 angry to neutral 을 구현할 수 있다고 생각하였다.(참고: [Unsupervised Speech Decomposition Via Triple Information Bottleneck](https://github.com/auspicious3000/SpeechSplit)) 인코더를 이용하여 melspectogram으로 변환한 음성정보에서 content 와 pitch, rhythm, identity등으로 분해하고 이를 다시 재조립시키는 모델을 학습하였다. 그래서 기존의 voice conversion이 가지고 있는 고질적인 문제인 speaker-dependent 과 independent information를 해결하였다.

## 4. 어떻게 학습 시켰는가?

팀원 한명의 음성정보를 학습시켜서 서로 다른 음성정보에 대한 감정변화에 대한 학습이 진행되는지 관찰하였다. 팀원 음성정보를 numpy와 melspectogram으로 쪼개서 다른 음성데이터와 함께 array로 저장하여 학습을 진행하였다. 음성 데이터는 조용한 상황에서 진행된 영어로 약 5분짜리의 음성들을 사이의 delay 시간 없이 깔끔하게 다듬은 데이터를 사용하였다. 이후 다시 음성을 재합성 하는데에는 필요한 음성 데이터 (약 2초짜리)를 동일한 방법으로 편집하여 기존에 존재하는 성우의 데이터와 감정을 넣은 데이터를 합쳐서 재합성하는 방식을 이용하였다.

## 5. 추후 개선점 

-  melspectogram에서 다시 음성으로 재합성을 시키는데 속도를 빠르게 개선시키자 
-  실시간으로 합성시키도록 하자
-  임의의 학습을 시키지 않은 음성정보에 대해서도 진행될 수 있도록 하자

