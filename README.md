# 패션 이커머스 플랫폼 데이터 기반 고객 행동 분석
- 구분: 개인 프로젝트
- 기간: 2024년 10월 31일 ~ 2024년 11월 8일

<br>

## 1. 문제 정의
패션 이커머스 플랫폼의 고객 행동 데이터를 분석하여 **구매 패턴과 충성도를 파악**하고, 이를 바탕으로 **전환율 개선과 이탈 방지 전략을 수립**하고자 한다.

이번 분석에서는 **추천 알고리즘의 효과성과 고객 세분화에 따른 퍼널 전환율 차이**를 분석하여 **맞춤형 마케팅 전략**을 도출하는 것이 목표이다.

<br>

## 2. 데이터 수집 및 분석

- **데이터 출처** : 데이터 분석가의 프로젝트(데.프) - 패션 이커머스 플랫폼 시뮬레이션 데이터
- **데이터 종류** : 사용자, 판매자, 상품, 로그인 로그, 상품 페이지 로그, 장바구니 로그, 구매 로그, 구매 상세 내역
- **데이터 기간** : 2018년 5월 1일 ~ 2023년 12월 31일

**⚙️ 데이터 전처리**
- 날짜 데이터가 object 타입으로 저장되어 있어 **5개 컬럼을 날짜 형식으로 변환**
- 상품 페이지 로그에서 **중복 2건**, 구매 상세 내역에서 **중복 26건** 제거

**📊 최근 지표**
- 최근 1년간 **매출, 구매 건수, 객단가 상승** 및 연말 프로모션 영향으로 **12월 성과 지표 급상승**
- **Stickiness도 12%에서 22%로 증가**하며 사용자 참여도 향상
- 코호트 분석 결과, **첫 구매 후 한 달 내 재구매율 증가**, 2~4개월 내 **약 30%로 안정화**
- **2월 이후 매출 감소** 경향이 나타나 **고객 이탈 방지 전략 필요**

**💡 분석 방법**
- 내부 추천 알고리즘이 **장바구니 전환율에 미치는 영향 분석**
- 리뷰 평점과 개수가 **구매 전환율에 미치는 영향 분석**
- 유저 세그먼트 기반 **이탈률 분석 및 주요 이탈 지점 파악**


<br>

## 3. 가설 설정 및 검증

### 가설 1 : 내부 추천 알고리즘으로 추천된 상품이 일반 상품보다 장바구니 전환율이 높을 것이다

**검증 방법** : 카이제곱 검정 수행

**검증 결과** :
- **장바구니 전환율** : 일반 상품 (31.09%) vs. 추천 상품 (30.76%)

  - 추천 여부와 장바구니 전환 여부 사이에 연관성이 없음 ❌ (p-value = 0.1683)
  - **추천 알고리즘이 고객의 장바구니 전환에 유의미한 영향을 미치지 않고 있음**

<br>

### 가설 2 : 리뷰 평점이 높거나 리뷰 개수가 많은 제품은 구매 전환율이 더 높을 것이다
-> 리뷰 평점이 높은 제품이 구매 전환율이 높다면 리뷰를 강조하는 디자인 ab테스트  
고평점/저평점 리뷰가 특정 가격대나 카테고리에 영향을 받았는지 분석

<br>

### 가설 3 : 유저 세그먼트를 분석하면 특정 그룹의 이탈률이 다른 그룹보다 높게 나타날 것이다

**유저 세그먼트 방법** : RFM 프레임워크를 활용한 K-means 클러스터링으로 고객 세분화 진행
- **Recency** : 2023-12-31 기준으로 최근 1개월 내 구매 여부
- **Frequency** : 2023년 총 주문 건수
- **Monetary** : 2023년 총 주문 금액
- 2023년에 구매 이력이 없는 고객은 휴면 고객으로 간주

엘보우 기법을 통해 군집 수를 4개로 설정했으며, 실루엣 계수는 0.63으로 나타남

<br>

**고객 군집별 RFM 시각화**

![07_고객세분화_rfm_시각화](https://github.com/user-attachments/assets/4f64c19a-d12f-4c37-bec0-7dab44b0b694)

- 군집 0 : 구매 빈도와 금액이 모두 낮은 **비활성 고객**
- 군집 1 : 중간 정도의 구매력을 가진 **활성 고객**
- 군집 2 : 주문 금액이 매우 높은 **프리미엄 고객**
- 군집 3 : 최근 주문 비율이 높으나 빈도와 금액은 낮은 **일시적 활성 고객**
- 군집 4 : 최근 1년간 구매 내역이 없는 **휴면 고객** (클러스터링에서 제외)

<br>

#### 고객 군집별 퍼널 분석
프리미엄 고객, 활성 고객, 일시적 활성 고객은 구매 및 재구매 전환율이 높게 나타났으며, 비활성 고객과 휴면 고객의 전환율은 아래와 같다.

![image](https://github.com/user-attachments/assets/b4d07671-c606-4e7d-b354-ad0c1c7a2520)

- **비활성 고객** : 최근 한 달간 구매 내역이 없고, **재구매율이 43.8%로 낮은 편** 🔺
- **휴면 고객** : 활동하지 않는 것처럼 보였지만, 85.8%가 상품 페이지를 방문했음에도 **구매로 이어지지 않음** ❌

<br>

## 4. 인사이트
- 현재 추천 알고리즘이 **장바구니 전환율을 효과적으로 증가시키지 못함**

- 비활성 고객은 재구매율이 낮아 **장기적 이탈 가능성이 높음**

- 휴면 고객은 상품 페이지를 방문하지만 구매로 전환되지 않아 **경험 개선이 필요함**

<br>

## 5. 결론 및 액션 제안

비활성 고객과 휴면 고객 군집은 낮은 전환율로 인해 충성도가 부족한 상태이며, 현재 추천 알고리즘이 고객의 장바구니 전환에 유의미한 영향을 미치지 않는 것으로 확인되었습니다. 이러한 문제를 개선하기 위해, **고객 충성도를 높이기 위한 맞춤형 프로모션**과 **추천 알고리즘의 개선**이 필요합니다. 아래 두 가지 제안을 통해 고객 전환율을 증가시키고 장기적인 고객 가치를 향상시키고자 합니다.

<br>

#### 비활성 고객과 휴면 고객의 복귀 시 할인 쿠폰 제공 여부에 따른 전환율 차이를 확인하는 A/B 테스트

- **가설** : 복귀 시 할인 쿠폰을 제공하면 비활성 고객과 휴면 고객의 구매 전환율이 증가할 것이다.
- **목적** : A/B 테스트를 통해 쿠폰 제공이 실제로 구매를 유도하는지 확인하고, 해당 고객군에 맞춘 프로모션 전략의 효과를 평가하여 향후 마케팅 전략에 반영합니다.


#### 새로운 추천 알고리즘 개발 후 장바구니 전환율 차이를 확인하는 A/B 테스트

- **가설** : 개선된 추천 알고리즘을 통해 추천된 상품이 기존 대비 장바구니에 더 많이 추가될 것이다.
- **추가 가설** : 추천된 상품이 장바구니에 추가되었을 때, 고객의 구매 전환율이 일반 상품보다 높을 것이다.
- **목적** : 휴면 고객의 경우 상품 페이지까지는 방문하였으나 장바구니로의 전환이 저조했던 문제를 해결하기 위해 고객의 이전 구매 기록과 관심 카테고리를 반영한 개인화 추천을 제공하여 장바구니 전환율을 높이는 방안을 테스트하고자 합니다. 추가 가설을 통해 장바구니에서 구매로의 전환에도 연관성이 있는지 확인할 수 있습니다.

<br>

## 6. 회고


| **✅ Keep** | **❌ Problem** | **🔍 Try** |
|---------|-----------|--------|
|  |  |  |
|  |  |  |
|  |  |  |
