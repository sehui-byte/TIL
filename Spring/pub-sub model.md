### pub-sub model

- publish-subscribe model
- 비동기식 메세징 패턴(Asynchronous Messaging Pattern)

>1. 우체부(Publisher)가 편지(Message)를 넣는다.
>2. 편지(Message)는 우체통(Broker or Channel)에 넣는다.
>3. 각 집의 호수(Topic)에 맞게끔 편지(Message)를 넣는다.
>4. 우리(Subscriber)는 우체통에 들어 있는 편지를 가져간다.
>
>출처: https://sugerent.tistory.com/585 [MISTERY]



![img](https://blog.kakaocdn.net/dn/cKeyq1/btqPWZ4SKt1/UWsEFT2UqfxgIsFjZkZcOk/img.png)



----------



### Kafka

- 링크드인에서 개발한 분산 메세징 시스템.
- MSA에서 서비스 간에 통신

- pub-sub model
  - publish : producer
  - subscribe : consumer




[이 링크](https://oingdaddy.tistory.com/274)를 참고하여 kafka를 설치하고, 예제를 따라해보았다.



1. **zookeeper 실행**

   ```
   zookeeper-server-start.bat ..\..\config\zookeeper.properties
   ```

   

2. **kafka 실행**

   ```
   kafka-server-start.bat ..\..\config\server.properties
   ```

   

3. **topic 생성**

```
kafka-topics.bat --create --bootstrap-server localhost:9092 --topic coffee
```

![image-20210705091758441](image/image-20210705091758441.png)

kafka-server에서 `topic`이 생성된 것을 확인할 수 있다.

![image-20210705091639438](image/image-20210705091639438.png)



4. producer

   ```
   >kafka-console-producer.bat --broker-list localhost:9092 --topic coffee
   >[메세지]
   ```

   

![image-20210705093127911](image/image-20210705093127911.png)

5. consumer

   ```
   kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic coffee --from-beginning
   ```

   

![image-20210705093057570](image/image-20210705093057570.png)

---------



### Spring Cloud Stream

- spring cloud stream application과 middleware시스템(kafka, RabbitMQ ...) 은 중간에 spring cloud stream이 제공하는 `binder`구현체를 두고 통신을 한다.

- `binder`의 경우 **spring이 설정을 읽어 미들웨어에 해당하는 binder를 구현체로 제공**해준다. `RabbitMQ`, `kafka`를 동시에 사용 가능하다.

  - **Processor(input, output)**
  - **Source(ouput)**
  - **Sink(input)**

  

  이 부분은 [이 글](https://coding-start.tistory.com/139)을 많이 참고하였다.

  

<img src="https://t1.daumcdn.net/cfile/tistory/990DED495C9C7A4B11" alt="img" style="zoom:67%;" />



------------

## 참고자료

- https://sugerent.tistory.com/585
- https://honglab.tistory.com/61
- https://needjarvis.tistory.com/598?category=925090
- **https://coding-start.tistory.com/139**
- **[springcloudstream과 kafka 연동하기](https://kamang-it.tistory.com/entry/KafkaJavaSpringBootSpringCloudStreamSpringCloudStream%EA%B3%BC-Kafka-%EC%97%B0%EB%8F%99%ED%95%98%EA%B8%B0?category=799882)**
- **[window 환경에 kafka설치하고 간단히 테스트 해보기](https://oingdaddy.tistory.com/274)**
- **[apache kafka 구축 - springboot 기반 msa](https://mr-spock.tistory.com/46)**
- [메시징 시스템의 이해](https://victorydntmd.tistory.com/343)