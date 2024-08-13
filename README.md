# 호갱예스

호갱예스는 부동산 실거래 정보를 조회 할 수 있는 서비스입니다.   
실제 서비스인 '호갱노노'를 참고하여 제작하였습니다.   

이 프로젝트는 두가지 모듈로 나뉩니다.

#### 1. [batch-estate-engine](https://github.com/dsadara/batch-estate-engine)

부동산 실거래 데이터를 수집하는 배치 모듈입니다.  
스키마를 변경하기 위한 마이그레이션 작업도 이곳에서 진행합니다.

#### 2. [hogang-yes-api](https://github.com/dsadara/hogang-yes-api)

부동산 데이터를 조회할 수 있는 API 입니다.   
추후 코드의 변경이 많을 모듈이기에 CI/CD를 적용했습니다.  

## 아키텍쳐

![hogang-yes-architecture drawio](https://github.com/user-attachments/assets/39f3c37c-7ba2-4182-80c1-f96c23815d6b)