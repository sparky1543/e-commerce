# 패션 이커머스 플랫폼 데이터 기반 고객 행동 분석
- 구분: 개인 프로젝트
- 기간: 2024년 10월 31일 ~ 2024년 11월 8일

<br>

## 1. 문제 정의

- 패션 이커머스 플랫폼에서는 다양한 고객이 상품을 탐색하고 구매하지만 **일부 고객층의 구매 전환율이 낮거나 장기적으로 이탈하는 문제**가 발생함
- 내부 추천 알고리즘과 리뷰 시스템이 고객의 구매 결정에 실질적으로 **긍정적인 영향을 주는지에 대한 검증**이 필요함

<br>

## 2. 데이터 수집 및 분석

- **데이터 출처** : 데이터 분석가의 프로젝트(데.프) - 패션 이커머스 플랫폼 시뮬레이션 데이터
- **데이터 종류** : 사용자, 판매자, 상품, 로그인 로그, 상품 페이지 로그, 장바구니 로그, 구매 로그, 구매 상세 내역
- **데이터 기간** : 2018년 5월 1일 ~ 2023년 12월 31일

**데이터 전처리**
- 날짜 데이터가 object 타입으로 저장되어 있어 **5개 컬럼을 날짜 형식으로 변환**
- 상품 페이지 로그에서 **중복 2건**, 구매 상세 내역에서 **중복 26건** 제거

**최근 지표**
- 최근 1년간 **매출, 구매 건수, 객단가 상승** 및 연말 프로모션 영향으로 **12월 성과 지표 급상승**
- **Stickiness도 12%에서 22%로 증가**하며 사용자 참여도 향상
- 코호트 분석 결과, **첫 구매 후 한 달 내 재구매율 증가**, 2~4개월 내 **약 30%로 안정화**
- **2월 이후 매출 감소** 경향이 나타나 **고객 이탈 방지 전략 필요**

**분석 방법**
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

**검증 방법** : 선형 회귀 분석 수행

**검증 결과** :

- **구매 전환율 설명력** : 리뷰 평점과 리뷰 개수는 구매 전환율을 거의 설명하지 못함 **(R² = 0.0008)**

- **회귀 계수 및 유의성** :

  - 리뷰 평점 (rating) : **-0.000034 (p = 0.9663)** → 구매 전환율에 유의미한 영향 없음 ❌
  - 리뷰 개수 (review_count): **0.000002 (p = 0.2684)** → 구매 전환율에 유의미한 영향 없음 ❌

- **모델 전체 유의성** : **(F-검정 p-value = 0.4425)** → 모델이 전체적으로 유의미하지 않음 ❌

  - **리뷰 평점과 개수는 구매 전환율을 설명하는 중요한 요소가 아닐 가능성이 높음**
  
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

- 리뷰 평점과 리뷰 개수는 **구매 전환율을 높이는 주요 요인이 아님**

- 비활성 고객은 재구매율이 낮아 **장기적 이탈 가능성이 높음**

- 휴면 고객은 상품 페이지를 방문하지만 구매로 전환되지 않아 **경험 개선이 필요함**

<br>

## 5. 결론 및 액션 제안

- **내부 추천 알고리즘이 장바구니 전환율을 효과적으로 높이지 못함**
<br> → 단순한 추천보다는 고객의 관심사 및 행동 데이터를 반영한 **개인화 추천 시스템 개선 필요**

- **리뷰 평점과 리뷰 개수는 구매 전환율에 유의미한 영향을 미치지 않음**
<br> → 리뷰 수를 늘리는 것이 아닌, **리뷰의 질적 향상**이 더 중요할 가능성이 높음

- **유저 세그먼트 분석 결과, 비활성 고객과 휴면 고객의 전환율이 현저히 낮음**
<br> → 이탈 가능성이 높은 고객군을 타겟으로 한 **재구매 유도 전략 필요**

<br>

### 액션 제안

#### 1. 추천 알고리즘 개선 및 A/B 테스트 진행
 
> 추천 알고리즘이 장바구니 전환율을 높이는 데 효과적이지 않음 → **개인화 추천 개선 필요**  
> **A/B 테스트**를 통해 기존 추천 방식 vs 개인화 추천 방식 비교  

**실행 방안**  
- **AI 기반 맞춤 추천 시스템 도입** : 조회/구매 내역, 선호 브랜드 반영  
- **비슷한 체형의 고객이 구매한 제품 추천 기능 추가**  
- **예시 :** **무신사** → AI 기반 선호도 반영 개인화 추천으로 전환율 상승  

<br>

#### 2. 포토 리뷰 및 스타일링 후기 활성화

> 리뷰 평점과 개수만으로 구매 전환율 증가 효과 적음 → **리뷰 질적 향상 필요**  
> 신뢰도 높은 리뷰를 **제품 상세 페이지 상위 노출 필요**  

**실행 방안**  
- **포토 리뷰 작성 시 추가 적립금 or 할인 쿠폰 제공**  
- **우수 포토 리뷰 공식 SNS 및 브랜드 페이지 노출**  
- **예시 :** **무신사** → 포토 후기, 스타일 후기 작성 고객에게 추가 적립금 제공

<br>

#### 3. 유저 세분화 기반 맞춤형 마케팅 실행

> 비활성 고객과 휴면 고객의 전환율 저조 → **유저 세그먼트별 차별화된 마케팅 필요**  

**실행 방안**  
- **비활성 고객 (재구매율 낮음)** : 리마인드 프로모션 진행  
  - **예시 :** **지그재그** → 특정 기간 미구매 고객 대상 한정 할인 쿠폰 제공  
- **휴면 고객 (구매 없이 상품 조회)** : 푸시 알림 & 개인화 메시지 발송  
  - **예시 :** **에이블리** → 찜한 상품 가격 인하 시 자동 알림 발송  

<br>

## 6. 대시보드

패션 이커머스 플랫폼의 고객 행동과 매출 성과를 분석하는 [태블로 대시보드](https://public.tableau.com/app/profile/siyoon.park/viz/e-commerce_17415108593680/1)를 구현하여 인사이트를 도출할 수 있도록 구성

![패션 이커머스 고객 및 매출 대시보드](https://github.com/user-attachments/assets/ece3d5b1-f783-467a-afcd-f1421c3e8461)

<br>

## 7. 회고

| **✔️ Keep**| **❌ Problem** | **🔍 Try** |
|------------------|-----------------|----------------|
| 다양한 분석 기법을 활용해 고객 행동을 입체적으로 분석한 점 | 추천 알고리즘의 작동 방식을 명확히 파악하지 못한 점 | 할인율, 브랜드 신뢰도 등 추가 변수 고려 |
| 유저 세그먼트 분석을 통해 고객 유형별 이탈 경향을 파악한 점 | 실제 UI/UX를 알지 못해 고객 경험을 파악하기 어려웠던 점 | 이메일, 푸시 알림 등 실제 마케팅 캠페인 효과 분석 |
| 실험 결과를 바탕으로 실무에 적용 가능한 액션을 도출한 점 | 프로모션이나 마케팅 영향이 충분히 고려되지 않은 점 | 패션 플랫폼 운영 사례 비교 및 추가 실험 설계 |





