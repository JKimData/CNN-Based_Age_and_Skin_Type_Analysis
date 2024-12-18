# 👩 CNN-Based Age and Skin Type Analysis
> **CNN 기반 나이 및 피부 분석을 통한 스킨테어 맞춤 솔루션** \
> Advisor: 민형기 교수님(한양대학교)

### 📌 프로젝트 소개
- 한국인 피부 상태 측정 데이터를 바탕으로 한국인 피부 상태 측정 데이터를 바탕으로 얼굴 이미지를 CNN 기반 딥러닝 모델로 분석하여 나이와 피부 타입을 예측하고, 이를 통해 맞춤형 스킨케어 제품을 추천하는 시스템을 구현합니다.
이를 통해 사용자의 피부 상태에 최적화된 제품을 추천하여 보다 효과적인 스킨케어를 지원합니다.

### 💻 프로젝트 자료  
- PPT 자료 첨부
- CNN 딥러닝 코드 자료 첨부
- 데이터 전처리 완료 data 첨부
- 화해 크롤링 데이터 수집 data 첨부
- 자료: 한국인 피부상태 측정 데이터 [LINK](https://www.aihub.or.kr/aihubdata/data/view.do?currMenu=115&topMenu=100&aihubDataSe=data&dataSetSn=71645) 

# 📑 프로젝트 결과물 소개

### **1️⃣ 데이터 소개** 

**✔ 데이터 요약**
- 데이터 이미지: 스마트폰 촬영 얼굴 정면 사진 총 645장
- 라벨링 데이터: age, skin_type, sesitive, angle 등
- 타겟 변수: age, skin_type
![image](https://github.com/user-attachments/assets/8ba6812e-794a-419c-b049-3586ec0d7464)

**✔ 데이터 전처리**
- skin_type 에서 중성 타입 제거 후, 피부 타입을 건성(0)과 지성(1)로 매핑하여 정리
- bbox 값으로 Pivot 분리하여 새로운 열 추가 후 id당 9개의 열을 1개의 열로 합침
- 이미지 데이터는 bbox 기준으로 자르고, 224*224 로 크기 조정 후 0~1 사이로 정규화

___

### **2️⃣ CNN 모델 및 학습 결과**
- 이미지의 각 부분(총 9개)을 개별적으로 분석하여 나이를 예측하고, 피부 타입은 0.5 이하일 경우 건성, 0.5 이상일 경우 지성으로 1차 분류
- 1차 분류 후 각 부분의 분석 결과를 평균하여 전체 이미지의 나이대와 피부타입을 결정함

![그림1](https://github.com/user-attachments/assets/b9ebd7eb-b1c5-46d2-bfa0-e036df5ab76b)

**✔ 모델 학습 결과**

![그림1](https://github.com/user-attachments/assets/a11d8559-6e50-4147-9a0b-d93c1d43c031)

- Train: Age MAE (4.66 - Loss: 7.21), Skin Type Accuracy(64.64 - Loss: 1.60), F1: 0.53, Recall: 0.46, Precision: 0.61, AUC: 0.69
- Test: Age MAE (7.68 - Loss: 19.29), Skin Type Accuracy(59.43 - Loss: 1.66), F1: 0.42, Recall: 0.24, Precision: 0.53, AUC: 0.60
- Train 데이터에서는 나이 예측과 피부타입 예측 모두 좋은 성능을 보이나, Test 데이터에서는 피부 타입 정확도가 낮아지고, Recall 이 현저히 떨어짐
- 과적합 가능성이 높으며, 이로 인해 모델의 일반화 성능이 다소 감소함
- 특히 피부 타입 예측 성능 향상을 위해 추가적인 모댈 개선 또는 파라미터 튜닝등을 계속해서 필요함

___

### **3️⃣ 화해 스킨케어 맞춤 솔루션**

**✔ 데이터 수집 및 크롤링**
- 화해 연령대별, 피부별, 카테고리별 Top 상품 100개씩 모두 데이터를 수집
- 상품 내 AI리뷰(좋은점, 아쉬운 점), 목적별 성분 등 상세 데이터 수집
- 총 2,942개 수집 완료

**✔ SQL을 통한 상품 리스트 추출**
- 연령대와 피부타입을 바탕으로 상품 리스트를 제공함
![image](https://github.com/user-attachments/assets/28a7cd9f-3de0-400e-ac75-d2a87b4bc830)

**✔ 맞춤 솔루션 데모(PPT)**
![image](https://github.com/user-attachments/assets/ee30ec54-08c1-4240-8cc0-f2771e4cbb66)
![image](https://github.com/user-attachments/assets/0704147f-ffb4-4ed8-9e51-7597757d86d0)

___

### **4️⃣ 프로젝트 결과**
 - 나이와 피부 타입 예측 가능: 나이 예측은 MAE 기준 4.6-7.7 정도의 차이를 나타내며 안정적인 성능을 보임
 - 피부 타입 정확도는 약 59.1% 수준으로 다소 낮으나 피부를 예측 가능한 모델로 구축을 완료함
 - 나이대와 피부 타입 정보를 활용해 화해 사이트에서 수집한 데이터를 연계하여 상품 추천 시스템을 구현함

  
