# catonator
This program transforms standard photographs into cartoon-style images using digital image processing techniques using opencv


## 1. 기술 및 알고리즘
Linear Intensity:  $I' = \alpha I + \beta$대비($\alpha=1.2$) 와 밝기($\beta=10$)를 높여 이미지의 시인성 확보 

HSV Saturation Boost 채도(S)와 밝기(V) 채널을 직접 조작하여 강렬한 색감 구현

선명도 보정:   사물의 형태가 뭉개지지 않도록 경계면을 날카롭게 보정

Bilateral Filter:  Edge는 보존하면서 면의 질감은 부드럽게 단순화하여 만화적 효과 부여

Canny Edge Detectio:  Gaussia Blur을 이용한 후 정교한 Edge를 추출하여 line drawing생성

## 2. Success Case
![rap_theory_final](https://github.com/user-attachments/assets/c9afb925-18a6-4a21-b300-f88c4e30593e)


특징
1. 강렬하고 생생한 색상 표현
  
2. 얇고 정교한 윤곽선
 
3. 캐릭터가 배경으로부터 확실히 분리되어 보임

## 3. Worst case
![image_theory_final](https://github.com/user-attachments/assets/ccb9414b-312c-45e1-8a9b-84b1085e3dd9)

1. 배경과 피사체의 구분실패 : 배경과 여우의 밝은 몸통 디테일이 사라지고 완전히 하얗게 변함

2. 윤곽선 불분명 : 여우의 몸체와 배경을 구분하는 외곽선이 뚜렷하게 연결되지 않고 끊기거나 희미함


## 4. 알고리즘의 한계
1. 고정 파라미터로 인한 데이터 손실: 현재 알고리즘은 모든 이미지에 동일한 선형 변환 ($I' = 1.2I + 10$) 을 적용한다 따라서 입력 이미지의 밝기 분포가 이미 한쪽으로 치우쳐 있는 경우, 픽셀 값이 최대치인 255를 초과하여 하얗게 날아가는 현상이 발생

2. 털과 같이 세밀한 변화가 많은 영역에서 Sharpening 필터가 인접 픽셀 간의 미세한 차이를 극대화하여 털의 질감을 노이즈로 변질시킨다.

3. 저대비 상황에서의 윤곽선 소실: Canny Edge Detection에 사용된 임계값(100, 200)이 고정되어 있어, 변화량이 이 기준을 넘지 못하는 경계선은 Edge가 아닌 것으로 판단되어 무시 됨

4. Limitations of Bilateral Filter: 피사체가 너무 복잡한 텍스처를 가지고 있으면, 필터가 이를 지워야 할 것이 아닌 보존해야 할 중요한 Edge로 오해 함


## Tech Stack
Language: Python 3.10.0

Library: OpenCV (Open-source Computer Vision Library) 4.13.0, numpy 2.2.6





