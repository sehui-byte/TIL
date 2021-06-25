

### MSA(Micro Service Architecture)



MSA는 모놀리식 아키텍처와 비교되어 설명되는데, 모놀리식은 소프트웨어의 모든 구성요소가 한 프로젝트에 통합되어있는 형태이다. 



MSA는 



![MSA(Microservice Architecture) | DEV Archive | YOONAH](https://yxxnah.github.io/2019/04/17/MSA-Microservice-Architecture-%ED%86%BA%EC%95%84%EB%B3%B4%EA%B8%B0-1/decentralised-data.png)

MSA는 각 컴포넌트가 서비스 형태로 구현되고, API를 이용하여 타서비스와 통신하게 된다. 또 각 서비스는 독립된 서버로 타 컴포넌트에 의존성이 없기 때문에 독립된 배포를 하게 된다. 그리고 서비스별로 별도의 DB를 사용한다. 





- MicroService Architecture

  - Inner Architecture
  - Outer Architecture
    - API GateWay
      - 사용자 인증(Consumer Identity Provider)
      - 권한 정책관리(Policy management)
    - Service Mesh
      - 마이크로서비스 구성요소 간의 네트워크 제어
    - Container Management
      - 대표적인 컨테이너 관리 환경 : 쿠버네티스
    - Backing Services
      - 어플리케이션이 실행되는 가운데 네트워크를 통해서 사용할 수 있는 모든 서비스.
      - Message Queue : Kafka
    - Telemetry
    - CI/CD Automation

  





---

### 참고자료

- https://velog.io/@tedigom/MSA-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-1-MSA%EC%9D%98-%EA%B8%B0%EB%B3%B8-%EA%B0%9C%EB%85%90-3sk28yrv0e

- https://velog.io/@tedigom/MSA-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-2-MSA-Outer-Architecure

- http://clipsoft.co.kr/wp/blog/%EB%A7%88%EC%9D%B4%ED%81%AC%EB%A1%9C%EC%84%9C%EB%B9%84%EC%8A%A4-%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98msa-%EA%B0%9C%EB%85%90/