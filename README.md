# Today I Learned(TIL)
## 05/21
## [spring boot]

### AdminUserController에서 User 객체를 이용해 멤버를 하나하나 복사해 와서 adminUser를 통해 전체 조회하는 예제를 실행해봄.

여기서 MappingJacksonValue 클래스가 어떤건지에 대해서 궁금해져서 알아보았다.

> MappingJacksonValue란?

MappingJacksonValue는 JSON Serialization(직렬화)을 처리하는 데 사용되며, 주로 Spring MVC(혹은 Spring  WebFlux) 기반의 웹 애플리케이션에서 Java 객체를 JSON으로 변환하거나, 반대로 JSON 데이터를 Java 객체로 변환하는 데 매우 효율적이고 강력한 라이브러리. 
 
일반적으로 컨트롤러 메서드에서 반환되는 데이터를 래핑하는데 사용되며, 이를 통해 특정 필터링 기능이나 시리얼라이제이션(Serialization) 설정을 적용하여 응답 데이터를 제어할 수 있습니다.

---

즉, 특정 사용자나 상황에 따라 다른 응답을 제공할 때 유용한 것이다. 
예제에서 보면 AdminUser 클래스의 "id", "name", "joinDate", "ssn"가 응답되도록 필터링을 했다.

이와 같이 하기 위해서는 AdminUser 클래스에 @JsonFilter("myDataFilter")와 같이 등록되어야 한다.

### Version 관리
- 실제 api를 쓰는것 처럼 버전을 만들어서 버전에 따른 출력값을 확인해 보았다.
- 첫번째는 URI를 통한 버전관리이다.
```python
@GetMapping("/v1/users/{id}")
```
- 두번째는 Request prarmeter 버전관리이다. 
```python
@GetMapping(value = "/users/{id}", params = "version=1")
```
params에 버전이름을 적어두면 된다.

호출은 다음과 같이 한다.
```
http://localhost:8088/admin/users/2?version=2
```
- 세번째는 headers 버전관리이다.
```python
@GetMapping(value = "/users/{id}", headers = "X-API-VERSION=1")
```
여기서부터는 URI를 통한 접근이 불가능하고, POSTMAN에 있는 header 기능을 이용하요 호출한다.
- 네번째는 mime-type 버전관리이다.
```python
@GetMapping(value = "/users/{id}", produces = "application/vnd.company.appv1+json")
```
> mime-type이란 : 특정한 파일이나 데이터가 어떤 유형인지 알려주는 형식

### 정리
(일반 브라우저에서 실행가능)

		1. URI를 통한 버전관리		(예시 사이트 : x)
		2. Request 파라미터 버전관리	(예시 사이트 : Amazon)

		(일반 브라우저에서 실행불가) - 직접프로그래밍 개발 or postman이용
		3. headers 버전관리			(예시 사이트 : Microsoft)
		4. mime-type 버전관리`		(예시 사이트 : GitHub)

### 버전관리를 하면서 주의할점
        1. uri를 통해 정보를 너무 과도하게 표기하지 말자.
		2. 잘못된 헤더값 사용 주의
		3. 인터넷 웹브라우저 캐시문제가 생길 수 있으니 캐시를 삭제해보고 다시 해보자


### Level3 단계의 REST API 구현을 위한 HATEOAS 적용

> HATEOAS란 : 현재 리소스와 연관된(호출 가능한) 자원 상태 정보를 제공해준다.

API를 설계 할 때는 RMM에서 말하는 레벨단계를 따라 API를 업데이트 할 수 있다.
```
	LEVEL 0
	LEVEL 1 : 리소스화 할 수 있는 단계, 리소스가 제공되고 있는 단계
	LEVEL 2 : HTTP에 필요한 상태코드, 메소드를 이용해서 리소스를 제공하는 단계   ( 사용자 관리, RESTFUL 지금까지 작업한 단계랑 같다고 보면 된다. )
	LEVEL 3 : HATEOAS 기능이 추가 / 연결되어 있는 단계 Hypermedia를 통해서 우리가 제공하고자 하는 리소스를 제어 하는 단계
```

HATEOAS를 사용하기 위해서는 pom.xml에 

```
    <dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-hateoas</artifactId>
	</dependency>
```
를 추가 해 주면 된다.



