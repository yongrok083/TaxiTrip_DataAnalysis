# Taxi_Trip_Data_Analysis

# 🚕 택시 데이터 분석 프로젝트

이 프로젝트는 NYC 택시(trip.csv) 데이터를 활용하여 **주행 시간**, **요금**, **거리**, **시간대별 패턴** 등을 분석하는 작업입니다.

---

## 📁 데이터셋 설명

- `trip.csv` 파일에는 다음과 같은 열이 포함되어 있습니다:

| 컬럼명 | 설명 |
|--------|------|
| `passenger_name` | 승객 이름 (전처리에서 제거됨) |
| `tpep_pickup_datetime` | 승차 시간 |
| `tpep_dropoff_datetime` | 하차 시간 |
| `payment_method` | 결제 수단 (현금, 카드 등) |
| `passenger_count` | 탑승 인원 수 |
| `trip_distance` | 주행 거리 (단위: km) |
| `fare_amount` | 기본 요금 |
| `tip_amount` | 팁 |
| `tolls_amount` | 통행료 |

---

## 🧹 1. 데이터 전처리

- **불필요한 열 제거**:
  ```python
  data.drop('passenger_name', axis=1, inplace=True)
결측치 처리 (fare_amount 평균으로 대체):


data['fare_amount'] = data['fare_amount'].fillna(data['fare_amount'].mean())
이상치 제거 (fare_amount가 400보다 큰 값 제거):


data = data[data['fare_amount'] <= 400]
컬럼명 변경 (가독성을 위해):


data.rename({'tpep_pickup_datetime': 'taxi_pickup_datetime', ...}, axis=1)
결제 수단 통일 (모든 카드 유형을 'Card'로 통합):


data['payment_method'] = data['payment_method'].apply(lambda x: 'Card' if 'Card' in x else x)

## ⏱️ 2. 주행 시간 계산
날짜형 변환 후, 주행 시간(초 단위) 계산:


data['trip_duration'] = (dropoff - pickup).dt.total_seconds()

## 📊 3. 파생 변수 생성
fare_per_min: 분당 요금

fare_per_km: km당 요금

pickup_hour: 승차 시각 (시간 단위)

## 📈 4. 데이터 시각화
Boxplot: 요금 이상치 시각화

Scatterplot: fare_amount와 trip_duration의 관계

Histplot: 시간대별 탑승 분포

