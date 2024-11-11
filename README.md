<a name="top"></a>

# 패션 이커머스 플랫폼 데이터 기반 고객 행동 분석
- 구분: 개인 프로젝트
- 기간: 2024년 10월 31일 ~ 2024년 11월 8일
<br>

<details>
  <summary>Table of Contents</summary>
  
  1. [프로젝트 개요](#프로젝트-개요)
  2. [데이터 설명](#데이터-설명)
  3. [문제 정의](#문제-정의)
      + [최근 1년간 성과 지표](#최근-1년간-성과-지표)
      + [최근 1년간 활성 사용자 지표](#최근-1년간-활성-사용자-지표)
      + [코호트 분석](#코호트-분석)
  4. [가설 설정 및 검정](#가설-설정-및-검정)
      + [가설 1](#가설-1)
      + [가설 2](#가설-2)
  5. [결론 및 제안](#결론-및-제안)

</details>

<br>


## 프로젝트 개요

패션 이커머스 플랫폼 데이터 분석을 통해 고객의 구매 행동을 이해하고 고객 충성도 강화를 위한 전략 수립을 목표로 합니다. 사용자 행동과 패턴을 바탕으로 고객 세분화, 리텐션, 구매력 등의 인사이트를 도출하고, A/B 테스트와 마케팅 전략 설계를 위한 데이터 기반 접근을 제공합니다.

<br>

## 데이터 설명

데이터 분석가의 프로젝트(데.프)에서 제공하는 패션 이커머스 플랫폼 시뮬레이션 데이터를 활용하여 사용자, 판매자, 상품, 로그인 로그, 상품 페이지 로그, 장바구니 로그, 구매 로그, 구매 상세 내역 데이터를 분석했습니다. 데이터 기간은 2018년 5월 1일부터 2023년 12월 31일까지입니다.

<br>

## 문제 정의

### 최근 1년간 성과 지표

![01_2023년_구매지표](https://github.com/user-attachments/assets/49f6a527-bf8d-43e0-a5e6-7a469341774d)

- 2023년 12월의 성과 지표가 크게 상승했으며 이는 연말 프로모션의 영향일 가능성이 큽니다.
- 이전 데이터를 확인해보면 1월까지 매출이 유지되다가 2월에 감소하는 경향이 확인됩니다.
- 시즌별 프로모션 전략을 강화하고, 연말에 유입된 고객이 이탈하지 않도록 방안을 마련해야 합니다.

<br>

### 최근 1년간 활성 사용자 지표

![스크린샷 2024-11-10 164737](https://github.com/user-attachments/assets/28526463-2ceb-4bc2-8a2c-5342a8d5d106)

- 활성 사용자는 꾸준히 증가하고 있으며 **stickiness도 1년간 12%에서 22%로 상승**하여 사용자 참여도 역시 꾸준히 향상되고 있습니다.
- 플랫폼의 지속 가능한 성장을 위해 **사용자당 매출 증대**와 **사용자 충성도 강화**를 통해 고객 가치를 높이고 경쟁 우위를 확보하는 전략이 필요합니다.

<br>

### 코호트 분석

2023년 첫 구매 월을 기준으로 코호트 분석을 통해 재구매율을 확인했습니다.

![05_코호트분석](https://github.com/user-attachments/assets/dc2dc4f8-71c7-4d19-b4e2-f1f282c34e0c)

- **첫 구매 후 한 달 내 재구매율이 하반기에 점차 증가**하며 연말 시즌의 영향을 받은 것으로 추정됩니다.
- 대부분의 코호트에서 **재구매율이 2~4개월 후 30%정도로 안정화**되는 경향이 나타납니다.
- 재구매율이 일정 수준에서 안정화되고 있으므로, 다음 목표는 **첫 구매 후 한 달 내 재구매율을 높여** 전체 재구매율을 더욱 증가시키는 것입니다.

<br>

> 💡 해당 플랫폼은 지난 6년간 꾸준히 성장해왔으며 최근 성과 지표가 크게 상승했습니다. 지속 가능한 성장을 위해 **고객의 재구매율을 높이고** **사용자 충성도를 강화**하여 경쟁 우위를 확보할 필요가 있습니다.

<h5 align="right"><a href="#top">⬆️TOP</a></h5>

## 가설 설정 및 검정

### 가설 1
#### 맞춤형 알고리즘으로 추천된 상품이 일반 상품보다 장바구니로 더 많이 전환될 것이다.

현재 고객 충성도 강화를 위해 내부 추천 알고리즘을 적용하고 있으며, 이 추천 알고리즘이 전환에 미치는 영향을 확인하기 위해 카이제곱 검정(Chi-square Test)을 진행했습니다.

- 전체 / 추천 / 일반 상품 뷰 대비 장바구니 전환율 : 30.97% / 30.76% / 31.09%

| 카이제곱 통계량 | p-value | 결과 |
| --- | --- | --- |
| 1.898 | 0.1683 | 추천 여부와 장바구니 전환 여부 사이에 연관성이 없음 |

추천된 상품이 장바구니 전환율을 높이지 않는다는 것은 현재 **추천 알고리즘이 고객의 장바구니 전환에 유의미한 영향을 미치지 않고 있음**을 의미합니다. 따라서 추천 알고리즘을 점검할 필요가 있습니다.

<br>

### 가설 2
#### 고객을 세분화하여 이탈률을 확인해보면 특정 그룹의 구매 단계에서 이탈률이 높을 것이다.

전체 고객을 대상으로 퍼널 분석을 진행한 결과, 특정 단계의 이탈률만으로는 적절한 액션을 결정하기 어려웠습니다. 이에 고객을 세분화하여 그룹별 퍼널 분석을 수행함으로써 보다 명확한 액션을 도출하고자 했습니다.

<br>

#### 고객 세분화

RFM 프레임워크를 활용한 K-means 클러스터링으로 고객 세분화 진행

- Recency : 2023-12-31 기준으로 최근 1개월 내 구매 여부
- Frequency : 2023년 총 주문 건수
- Monetary : 2023년 총 주문 금액

2023년에 구매 이력이 없는 고객은 추가 군집에 분류하여 휴면 고객으로 간주했습니다. 엘보우 기법을 통해 군집 수를 4개로 설정했으며, 실루엣 계수는 0.63으로 나타났습니다.

<br>

#### 고객 군집별 RFM 시각화

![07_고객세분화_rfm_시각화](https://github.com/user-attachments/assets/4f64c19a-d12f-4c37-bec0-7dab44b0b694)

- 군집 0 : 구매 빈도와 금액이 모두 낮은 **비활성 고객**
- 군집 1 : 중간 정도의 구매 빈도와 금액을 보이며 일정한 구매력을 가진 **활성 고객**
- 군집 2 : 모든 지표에서 높은 수치를 보이며 주문 금액이 매우 높은 **프리미엄 고객**
- 군집 3 : 최근 주문 비율이 높으나 빈도와 금액은 낮은 **일시적인 활성 고객**
- 군집 4 : 최근 1년간 구매 내역이 없는 **휴면 고객**이며, 클러스터링에서는 제외

<br>

#### 고객 군집별 퍼널 분석

군집 1과 군집 2는 모든 퍼널 단계에서 100%의 전환율을 기록했습니다. 군집 3은 재구매 단계에서만 14.4%의 이탈률을 보였고, 나머지 단계에서는 모두 전환되었습니다. 아래는 군집 0과 군집 4의 전환율 그래프입니다.

![image](https://github.com/user-attachments/assets/b4d07671-c606-4e7d-b354-ad0c1c7a2520)

- **군집 0 (비활성 고객)** : 최근 한 달간 구매 내역이 없고, 다른 군집에 비해 재구매율이 낮아 충성도가 부족한 고객군입니다. 장기적인 관점에서 이탈 가능성이 높으며 **충성도 강화와 재구매 유도를 위한 전략**이 필요합니다.
- **군집 4 (휴면 고객)** : 처음에는 전혀 활동이 없는 고객군으로 보였으나, 실제로 85.8%의 고객들이 상품 페이지까지는 방문하고 있습니다. 그러나 장바구니 전환율이 42.8%로 낮고 구매 단계에서는 전환이 전혀 이루어지지 않았습니다. 이는 **고객 경험의 불만족으로 구매가 이루어지지 않았을 가능성**이 있습니다.

<h5 align="right"><a href="#top">⬆️TOP</a></h5>

## 결론 및 제안

비활성 고객과 휴면 고객 군집은 낮은 전환율로 인해 충성도가 부족한 상태이며, 현재 추천 알고리즘이 고객의 장바구니 전환에 유의미한 영향을 미치지 않는 것으로 확인되었습니다. 이러한 문제를 개선하기 위해, **고객 충성도를 높이기 위한 맞춤형 프로모션**과 **추천 알고리즘의 개선**이 필요합니다. 아래 두 가지 제안을 통해 고객 전환율을 증가시키고 장기적인 고객 가치를 향상시키고자 합니다.

<br>

#### 비활성 고객과 휴면 고객의 복귀 시 할인 쿠폰 제공 여부에 따른 전환율 차이를 확인하는 A/B 테스트

- **가설** : 복귀 시 할인 쿠폰을 제공하면 비활성 고객과 휴면 고객의 구매 전환율이 증가할 것이다.
- **목적** : A/B 테스트를 통해 쿠폰 제공이 실제로 구매를 유도하는지 확인하고, 해당 고객군에 맞춘 프로모션 전략의 효과를 평가하여 향후 마케팅 전략에 반영합니다.


#### 새로운 추천 알고리즘 개발 후 장바구니 전환율 차이를 확인하는 A/B 테스트

- **가설** : 개선된 추천 알고리즘을 통해 추천된 상품이 기존 대비 장바구니에 더 많이 추가될 것이다.
- **추가 가설** : 추천된 상품이 장바구니에 추가되었을 때, 고객의 구매 전환율이 일반 상품보다 높을 것이다.
- **목적** : 휴면 고객의 경우 상품 페이지까지는 방문하였으나 장바구니로의 전환이 저조했던 문제를 해결하기 위해 고객의 이전 구매 기록과 관심 카테고리를 반영한 개인화 추천을 제공하여 장바구니 전환율을 높이는 방안을 테스트하고자 합니다. 추가 가설을 통해 장바구니에서 구매로의 전환에도 연관성이 있는지 확인할 수 있습니다.

<h5 align="right"><a href="#top">⬆️TOP</a></h5>
