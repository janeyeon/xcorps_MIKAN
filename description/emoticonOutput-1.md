#1. 사용한 모델 

U-GAT-IT 모델을 사용하였다. 

구현하고자 하는 목표는 사람얼굴을 인식하여 다른 형태로 변화하는 것이었다. 그중에서도 현재 가장 연구가 활발하게 진행되고 있는 사람에서 애니메이션으로의 변환이 가장 잘 이루어 질 것이라고 예상하였고, 많은 모델 중에서도 '선' 을 잘 구분할 수있는 U-GAT-IT이라는 모델을 사용하였다. 

초기 Stylization 방법에는 BN에 쓰였으나, Ulyanov가 BN layer를 IN layer로 대체해 큰 성과를 낼 수 있음을 알게 되었다. IN은 픽셀 공간에서 실행되는 Contrast normalization(대비 표준화)와 달리 feature 공간에서 일어나기 때문에 좀 더 큰 영향력을 가지므로 이전의 연구에서 평균, 분산과 같은 통계량을 매칭하는 것이 Style transfer에 효과가 있다는 점을 참고해 시작하였다. 

① **Attention 모듈**은 auxiliary classifier를 통해 얻은 attention map을 기반으로 Src 이미지와 Target 이미지의 차이, 즉 중요한 영역에 더욱 집중할 수 있도록 하였다. 

②**AdaLIN**(Adaptive Layer-Instance Normalization)을 통해 shape와 texture(style) 변화 모두에 대응할 수 있는 모델이다. 

이 두가지 특징을 가지고 Unsupervised image-to-image translation 방법을 개발한 것이 U-GAT-IT 모델이다. 아래의 링크를 클릭하면 실제 사용한 github 사이트로 연결된다.

[U-GAT-IT](https://github.com/znxlwm/UGATIT-pytorch)

#2. 왜 유미의 세포들인가?

-  선이 깔끔하고 두꺼워 선을 구현하기가 수월하였다. 
-  딥러닝 모델이 표현하기 어려운 코의 형태가 거의 없는 편이다. 
-  색의 사용이 간결하여 모델이 직접 따라하기가 쉬웠다. 

#3. 구현방법

A: <유미의 세포들> 웹툰에서 770개의 256px256px짜리 얼굴 그림을 캡처해 훈련시켰고, 20개의 얼굴 그림을 이용해 테스트했다.
B: 연령별, 성별별 아시아인의 얼굴을 크롤링한 AFAD-dataset에서 20-30세여성의 사진 중 크기가 256px256px 이상인 것들을 골라 크롭해 2000개를 이용해 훈련시켰고, 테스트할 때 쓴 사진의 개수는 40개이다. 총 74000번의 훈련을 거쳤다.

60000번째 반복 후 테스트한 그림 결과에서 머리카락에 존재하는 텍스처는 사진에 일반적이지 않은 요소가 있는 경우 나타나는 것이다. 머리카락의
세로 하이라이트, 핸드폰, 손가락 등이 그러한 요소이다. 또, 웹툰 <유미의 세포들>의 주인공 유미가 앞머리가 있는 금발의 얼굴이어서 데이터셋의 분포에서 그러한 얼굴의 비율이 가장 컸다. 70000번째 반복할 때의 결과와 같이 원래 사진이 흑발에 앞머리가 없는데도 불구하고 금발에 앞머리가 있는 그림으로 결과가 도출되는 경우가 종종 발생하였다.

#4. 주의사항

-  영상을 넣을 경우에는 .m4a 형태로 1~2초내의 짧은 영상으로 진행하는 것이 좋다. 
-  사진은 얼굴 위주로 머리카락 등이 안나오는 편이 모델이 더 잘 학습할 수 있다. 특히 안경과 앞머리등 얼굴에 있는 부가적 요소가 없는 편이 진행이 잘된다. 그리고 얼굴 표정의 변화가 너무 크지 않는 정면이 좋다.
-  색 등은 너무 강렬하지 않은걸 사용하는게 나으며, 사진의 사이즈 자체는 크게 상관 없다.