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
이미지 파일과 마스크 파일의 수가 동일하지 않아 문제점을 확인해야 한다.
이미지, 마스크 파일의 이름이 쌍을 이루지 않는 것을 찾아내고 파일명이 사진이 아닌 것을 제거한다.
같은 파일이 2개인 것을 제거한다.

<img src="https://user-images.githubusercontent.com/97801319/211377840-027793f6-0e79-4001-aba5-4e49bb02193f.png" width="500">

<img src="https://user-images.githubusercontent.com/97801319/211377887-7a76fdce-6b84-4fbe-b8ed-e51f6c2dbb43.png" width="300"><img src="https://user-images.githubusercontent.com/97801319/211377941-12d459c0-d3eb-4def-a208-e57fcf971083.png" width="500">

## 3. 분석 모델, Unet

