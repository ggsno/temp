# 시계열 차트
[데모 페이지](https://time-series-chart.vercel.app/)

![녹화_2023_03_17_01_46_48_858](https://user-images.githubusercontent.com/46833758/225692376-6a014739-942d-47e7-917a-21d1f2c87eeb.gif)

1.시계열 차트 구현
- [x] 주어진 JSON 데이터의 `key`값(시간)을 기반으로 시계열 차트를 만들어주세요
  - 하나의 차트안에 Area 형태의 그래프와 Bar 형태의 그래프가 모두 존재하는 복합 그래프로 만들어주세요
  - Area 그래프의 기준값은 `value_area` 값을 이용해주세요
  - Bar 그래프의 기준값은 `value_bar` 값을 이용해주세요
  - 차트의 Y축에 대략적인 수치를 표현해주세요
2. 호버 기능 구현
  - [x] 특정 데이터 구역에 마우스 호버시 `id, value_area, value_bar` 데이터를 툴팁 형태로 제공해주세요

3. 필터링 기능 구현
  - [x] 필터링 기능을 구현해주세요, 필터링은 특정 데이터를 하이라이트 하는 방식으로 구현해주세요
    - 필터링 기능은 버튼 형태로 ID값(지역이름)을 이용해주세요
    - 필터링 시 버튼에서 선택한 ID값과 동일한 ID값을 가진 데이터 구역만 하이라이트 처리를 해주세요
  - [x] 특정 데이터 구역을 클릭 시에도 필터링 기능과 동일한 형태로 동일한 ID값을 가진 데이터 구역을 하이라이트해주세요


## 주안점

### 가시성 개선 및 재사용성 고려
- 일반적 사용(재사용)을 위해 모킹데이터에 기준을 두지 않고 일반적인 파라미터를 받기 위해 고민했습니다.
  - x축 데이터 배열과 좌,우측 y축 데이터 이름과 데이터 배열을 파라미터로 두고 그에 맞춰 모킹데이터를 변환해 사용
- 쉬운 이해를 위해 꼭 필요한 코드 이외의 다른 로직을 모두 제거하고 응집도를 최대한 높였습니다.
- 두 데이터셋의 y축 백분율 범위가 비슷할 때 많이 겹쳐보여 가시성이 떨어졌습니다. 하나의 데이터 셋에 두 배의 max값을 부여해 두 데이터셋을 상하로 나누어 보여줬습니다.
  - 이를 현재 목업 데이터에 의존하지 않기 위해 min값과 max값을 partial로 전달 할 수 있게 구현했습니다.

## 기타
### 필터링 상태 관리에 대한 고민
- 현재 필터링 정보는 useState로 관리하고 있습니다. 
- 필터링 정보를 url 쿼리스트링에 저장하는 방법도 고민했지만 다음의 이유로 보류했습니다. 
  - 데이터차트는 주로 관리자 페이지의 대시보드에서 사용할 것이라 생각했습니다. 
  - 대시보드에는 여러 차트가 있을 것이고 각각의 필터들을 url 쿼리스트링으로 관리하는 것은 무리일 것 같습니다.
  - 이커머스 사이트같이 필터링을 url로 공유하는 경우도 데이터차트에서는 드물 것이라 생각했습니다.
