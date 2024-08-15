# 호갱예스 (HogangYes)

호갱예스는 **부동산 실거래 정보를 조회**하는 서비스입니다.  
아파트, 단독주택, 다가구주택, 연립주택, 다세대주택, 오피스텔 종류별로 **약 2000만 건의 실거래 데이터**를 조회할 수 있습니다.  
[Swagger 명세서](http://3.37.47.2/swagger-ui/index.html)로 기능을 테스트해 볼 수 있습니다.

*p.s. 호갱예스는 실제 서비스인 호갱노노와 같이 훌륭한 서비스를 만들고자 지은 이름입니다.* 🙂

이 프로젝트는 **2개의 모듈**로 구성되어 있습니다.

### [1. batch-estate-engine](https://github.com/dsadara/batch-estate-engine)

일괄 처리로 부동산 데이터를 수집하는 모듈입니다. **Spring Batch의 chunk 지향 처리 기능**을 사용하여 구현했습니다.

chunk 지향 처리를 담당하는 step은 3가지로 구성되어 있습니다.

1. **ItemReader**: 공공데이터포털 API를 호출해서 얻은 Json 데이터를 DTO로 파싱합니다.
2. **ItemProcessor**: DTO를 Entity로 변환합니다.
3. **ItemWriter**: chunk size만큼 Entity가 모이면 한 번에 트랜잭션을 진행하여 데이터베이스에 저장합니다.   

또한 테이블 최적화를 수행하기 위해 **Flyway로 마이그레이션**을 진행하였습니다.

### [2. hogang-yes-api](https://github.com/dsadara/hogang-yes-api)

부동산 데이터를 조회하는 API 입니다. Spring MVC로 사용자의 HTTP 요청을 처리합니다.   

추후 코드의 변경이 많을 수 있다 판단이 들어서 CI/CD를 도입했습니다.   
Travis CI로 **자동 빌드**를 구현했고, Amazon S3, Amazon CodeDeploy로 **자동 배포**를 구현했습니다.   

또한 Ngnix의 리버스 프록시 기능을 사용하여 **무중단 배포**를 구축했고 서비스의 다운타임을 최소화 했습니다.   

## 아키텍쳐

![hogang-yes-architecture drawio](https://github.com/user-attachments/assets/39f3c37c-7ba2-4182-80c1-f96c23815d6b)

## 문제 해결 과정

**[1. 데이터 테이블 최적화](https://github.com/dsadara/batch-estate-engine/wiki/1.-%EB%8D%B0%EC%9D%B4%ED%84%B0-%ED%85%8C%EC%9D%B4%EB%B8%94-%EC%84%A4%EA%B3%84**):** 테이블의 컬럼 최적화와 정규화를 진행한 과정

**[2. 데이터 마이그레이션](https://github.com/dsadara/batch-estate-engine/wiki/2.-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EB%A7%88%EC%9D%B4%EA%B7%B8%EB%A0%88%EC%9D%B4%EC%85%98):** flyway 사용 중 트러블슈팅

**[3. 재실행 문제](https://github.com/dsadara/batch-estate-engine/wiki/3.-%EC%9E%AC%EC%8B%A4%ED%96%89-%EB%AC%B8%EC%A0%9C):** Spring Batch Job의 재실행 문제 해결

## 데이터베이스 스키마

## 시퀀스 다이어그램