# Dacon dielectric prediction

첫 데이콘 경진대회에 참여해서 좋은 결과를 낼 수 있었음.  
3등과 같은 정확도를 보였지만 조금 늦게 제출한 탓에 최종순위 5위로 마감.  

## 데이터 설명

+ train.csv
  + 개체정보
  > father: 개체의 가계 고유 변호  
  > mother: 개체의 모계 고유 변호  
  > gender: 개체 성별 (0 : Unknown, 1 : female, 2 : male)  
  > trait: 개체 표현형 정보
  + 15개의 SNP의 정보
  > snp_01 ~ snp_15
  + class: 개체의 품종(분류 대상)
  > A,B,C

+ snp_info.csv
  + 15개의 SNP의 세부정보
  > name: SNP 명  
  > chrom: 염색체 정보  
  > cm: Genetic distance  
  > pos: 각 마커의 유전체상 위치 정보  

상위데이터들로 이루어져 있다.  

-----------------------------------------------------------------------------------   

## 분석방법

### **데이터 전처리**

- 데이터를 각 항목별로 시각화해서 어떠한 특징이 있는지 파악
- 파생변수 이용(비슷한 SNP 정보를 모아서 새로운 변수 생성) -> 성능에 향상에 **효과 X**  
- 처음에는 큰 부분을 시각화하여 살펴봤고 뒤에서는 SNP에서 특징이 있는 것만 뽑아내 특징을 다시 파악  
- 히트맵도 그려 변수간의 상관관계를 파악했다.  

![011](https://github.com/Taeyoungleee/Dacon-dielectric-prediction/assets/113446739/502baed1-1fdf-406e-b126-aa1c687d74a9)

![012](https://github.com/Taeyoungleee/Dacon-dielectric-prediction/assets/113446739/c5aa6dc3-9c13-493e-b31a-5c44bdb3d552)

![상관계수](https://github.com/Taeyoungleee/Dacon-dielectric-prediction/assets/113446739/9334a9c2-174d-4c69-aba9-91a7be184983)

- chrom이 가장 많은 데이터를 기준으로 유전체 종류를 분류하는데 가장 큰 영향을 줄거 같은 데이터만 남겨 분류하는데 사용  
- 문자형인 snp데이터를 **LabelEncoder**를 통해 숫자형으로 바꿔주고 버릴 column들을 정해 제외  
- 대회의 취지에 맞게 보다 더 적은 SNP 정보로 높은 분류 성능을 내기 위해 노력  

### **사용한 라이브러리 및 머신러닝 모델**  

+ **AutoML**  
> Automated Machine Learning의 줄임말로, 머신러닝 모델 개발, 배포등을 자동으로 처리할 수 있게 도와주는 프로세스이다.  
> **PyCaret** 이라는 라이브러리를 사용  
> [PyCaret 홈페이지](https://pycaret.gitbook.io/docs/)

+ 라이브러리 사용후 나온 상위모델 5가지
> Decision Tree Classifier  
> Ridge Classifier  
> Extra Trees Classifier  
> Random Forest Classifier  
> Gradient Boosting Classifier  

상위모델에서 **Ridge Classifier**를 선택해 제출  
(Macro F1 Score가 대회 점수산정의 기준이다.)  

-----------------------------------------------------------------------------------   

## 결과

+ 비교적 간단하게 분석했지만 대회 취지에 맞추기위해 노력 그 결과 좋은 성과가 나온것으로 판단  
+ AutoML을 사용해 모델을 만들었는데 생각보다 높은 정확도를 보여줬음을 알 수 있었음  
+ 향후에 더 복잡한 분석을 할 경우에도 AutoML을 활용해 분석해도 나쁘지 않을 것이라고 생각됨    

![데이콘 인증서](https://github.com/Taeyoungleee/Dacon-dielectric-prediction/assets/113446739/2a98339a-685b-4065-9123-7234a3f7fbbe)

