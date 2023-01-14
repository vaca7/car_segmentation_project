# 자동차 외관 손상 인식 자동화
기업 협업 프로젝트로 기업에서 제공 받은 자료로 중고차 산업, 차량 수리 업체 등과 같이 외관 손상을 판별해 내야하는 업종에서 외관 손상 인식을 자동화하여 육안으로 놓칠 수 있는 손상을 인식해줄 것입니다. 
<img src="이미지링크" width="500">
## 1. 데이터
기업에서 제공한 이미지
- 약 3000개의 차량 스크래치 이미지
- 약 3000개의 차량 스크래치 마스크 이미지

<img src="https://user-images.githubusercontent.com/97801319/211315179-7ea2c1ea-0a0b-4785-93e1-5384b035a1df.png" width="200"><img src="https://user-images.githubusercontent.com/97801319/211315327-ce3fb8a0-6a8e-4dce-b669-843997ccff97.png" width="200">
<img src="https://user-images.githubusercontent.com/97801319/211376993-2d25bca7-1be9-4697-8109-03850864074d.png" width="500">

## 2. 데이터 전처리
이미지 파일과 마스크 파일의 수가 동일하지 않아 문제점을 확인해야 합니다.
이미지, 마스크 파일의 이름이 쌍을 이루지 않는 것을 찾아내고 파일명이 사진이 아닌 것을 제거합니다.
같은 파일이 2개인 것을 제거합니다.

<img src="https://user-images.githubusercontent.com/97801319/211377840-027793f6-0e79-4001-aba5-4e49bb02193f.png" width="500">

<img src="https://user-images.githubusercontent.com/97801319/211377887-7a76fdce-6b84-4fbe-b8ed-e51f6c2dbb43.png" width="300"><img src="https://user-images.githubusercontent.com/97801319/211377941-12d459c0-d3eb-4def-a208-e57fcf971083.png" width="500">

## 3. 분석 모델, Unet
자동차 외관 손상은 그림에서 매우 작아 픽셀 단위로 구분해주는 Segmentation 기술을 사용할 것입니다. 그 중에서 대표적인 모델인 Unet을 사용합니다.

<img src="https://user-images.githubusercontent.com/97801319/211794499-cfdbc6c1-8743-4546-b20a-07712eea8967.png" width="500">

**-Unet 선택 이유**

U-Net은 'U-Net: Convolutional Networks for Biomedical Image Segmentation' 이라는 논문에서 제안한 구조로서 매우 적은 수의 학습 데이터로도 정확한 이미지 세그멘테이션 성능을 보여주어 주어진 데이터가 적은 저에게 적합하다고 판단했습니다.

또한 차량의 스크래치와 비슷한 MRI 이미지 분석에도 사용 되는 것을 보고 Unet 모델을 선택했습니다.

## 4. 손실 함수, Dice Loss
<img src="https://user-images.githubusercontent.com/97801319/211905105-3e51c7ba-74e8-4c96-a981-c5de9fc284a4.png" width="500">

**적용 이유**

- 분할 이미지에서 각각의 클래스 양이 불균형하면 적게 분포하는 클래스는 예측하지 않는 방향으로 학습이 진행되게 됩니다. Dice Loss를 사용하면 이 같은 문제를 해결할 수 있습니다.

## 5. 데이터 이미지 증강
기본적으로 부족한 데이터 양을 보완하기 위해 이미지 증강을 해주었습니다. 

<img src="https://user-images.githubusercontent.com/97801319/211796853-15610cfe-2b46-4b01-83ee-ad3d78568246.png" width="500">

## 6. 결과

**Dice Score : 0.341**

<img src="https://user-images.githubusercontent.com/97801319/211906095-fd1c243e-6202-481c-bdf8-8c3485e7ccd7.png" width="500">
<img src="https://user-images.githubusercontent.com/97801319/211909331-071661f4-9863-4ac4-a525-2a5b2a84f7bc.png" width="500">

## 7. 한계점 및 해결방안

 결과로 Score가 그리 높게 나오지 않아서 예측이 정확하게 되지 않는 것을 알 수 있습니다.
 점수가 낮게 나온것은 여러가지 이유가 있겠지만 제가 생각한 가장 큰 이유는 데이터의 부족입니다. 
 그 외 문제점들을 생각해보면
 
 첫 번째로, 과적합입니다. 위 그래프를 보면 과적합이 된것을 알 수 있습니다.
 해결방안으로는 Unet 모델을 직접설계 하는 것입니다. Dropout layer 추가하여 과적합을 방지할 수 있을것입니다.
 
 두 번째로, 낮은 반사된 빛이 스크래치로 인식되는 경우입니다.
 
 <img src="https://user-images.githubusercontent.com/97801319/211910810-5210775d-596a-4592-97b5-258ba3e36d10.png" width="500">
 
 위 그림처럼 반짝이거나 빛이 반사 되면 스크래치로 인식하는 경우가 있습니다. 
 해결방안으로는 homomorphic filter를 사용하는 것입니다. 이 필터는 이미지에서 조명을 제거해주는 역할을 하여 부족한 부분을 보완할 수 있을 것입니다.


