## 1. 사용한 모델

초기에 음성 변환을 위하여 사용한 모델은 cycleGAN을 이용한 감정변조였다. (참고:  [Emotional Voice Conversion and/or Speaker Identity Conversion with Non-Parallel Training Data](https://github.com/KunZhou9646/emotional-voice-conversion-with-CycleGAN-and-CWT-for-Spectrum-and-F0) ) 

parallel data set으로 진행한게 아니라 한 음성 content에 대해서만 학습을 진행한 것이 아니라서 

## 2. 왜 문제가 생겼는가?

다른 감정의 음성을 학습하여 그 감정정보를 빼주는게 아니라 두 domain의 차이점이 감정정보밖에 없었기 때문에 학습을 잘 진행할 수 있었던 것이었다. 

## 3. 왜 SpeechSplit 인가?

이건 직접 해당 정보를 분해해서 진행하는 거라서 ㄱㅊ다고 생각함

## 4. 어떻게 학습 시켰는가?

팀원 한명의 음성정보를 학습시켜서 서로 다른 음성정보에 대한 감정변화에 대한 학습이 진행되는지 관찰 

## 5. 추후 개선점 

-  melspectogram에서 다시 음성으로 재합성을 시키는데 속도를 빠르게 개선시키자 
-  실시간으로 합성시키도록 하자
-  임의의 학습을 시키지 않은 음성정보에 대해서도 진행될 수 있도록 하자

