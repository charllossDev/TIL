# MG Trial Api Performance
#### Mg시승보험 Api 성능 이슈 건(시승보험 조회, 계약, 계약취소) 기능

---
MG손해보험에 응답받는 API 속도가 현저하게 느린 이슈

* 평균 응답 속도 8 ~ 10초
* 빠를 경우 4 ~ 8초, 늦을 경우 30초를 초과하는 상당한 시간이 소요

문제점:

* MG손해보험으로부터 시승보험 정보를 늦게 받아 카플래너 App에서 속도 지연 및 딜레이 발생
* 과도한 대기 시간이 발생하여 서비스 장애 초래
* CarPlanner App과 CarPlanner Server의 Session Timeout 발생(10s) - Mg 시승보험 정보 유실
* 시승보험 데이터 신뢰도 하락 or 데이터 유실 발생

해결책:

### 시승보험 조회

* MG시승보험 조회 응답이 늦을 경우 장애 알림 팝업 호출 후 재시도 유도

### 시승보험 계약 체결

* PG결제 완료와, MG시승보험 계약 체결 서비스 분리
  + PG결제 완료 시 -> 시승보험 결제 내역 페이지 이동
  + 시승보험 결제 내역 페이지(상시 페이지 Refresh)
  + 시승보험 상태 추가(시승보험 심사 중)
  + CarPlanner Server에서 비동기 계약체결 처리

### 시승보험 계약 취소

* 실시간 계약 취소 상태 변경 후, 비동기 처리