# Today I Learned(TIL)
## 05/21

## [AWS]
### 클라우드 컴퓨팅
인터넷을 사용해서 공유자원(서버, 네트워크, 스토리지)을 사용할 수 있는 서비스이다.

데이터센터안에 네트워크장비가 있어서 우리가 장비들을 쓸 수가 있는 건데,
인터넷을 연결하면 라우터를 포함한 모든 네트워크장비를 쓸 수 있다.

또한 원래 우분투, 리눅스, 아마존을 쓰려면 가상머신을 깔아야 한다. 그러려면 용량이 큰 컴퓨터를 사야 하는데 클라우드 컴퓨팅은 이러한 모든 작업을 서비스 형태로 제공한다. 오직 인터넷에서 제공하는 서비스를 호출하여 즉시 필요한 자원을 사용할수 있다.

#### 클라우드의 특징
- 한 화면에 운영체제를 여러 개 띄워서 사용 할 수 있다.

#### 클라우드의 종류
- Amazon AWS
- Microsoft Azure
- Google Cloud Platform

### On demand 서비스와 SLA
> On demand

클라우드 서비스 사용자가 요청한 만큼 서비스를 제공하고 비용을 청구하는 모델이다.

대용량 서버중에서 요청한 만큼의 서버만을 사용자에게 제공하기 때문에 해당 서버의 자원을 분할, 할당할 수 있는 방법이 있어야한다.

즉, 가상화 기술이 필요하다.


> SLA(Service Level Agreement)

On demand 서비스 사용할 때 클라우드 컴퓨팅 서비스 사용자와 서비스 제공자(AWS) 간에 서비스 수준에 대한 협약서.  
즉, SLA를 통해서 사용한 서비스만큼 비용을 지불하게 된다.

### 가상화
하드웨어를 분할하거나 할당할 수 있어서  
한 대의 서버를 여러 서비스 사용자가 물리적으로 같이 사용할 수 있다.   
(한대의 고성능 컴퓨터를 분할하여 여러명이 쓸 수 있다.)       

또한 여러개의 물리적 자원을 통합하여 하나의 컴퓨터처럼 사용할 수 있다.  
(마치 한대의 고성능 컴퓨터를 사용하는 것처럼 여러개의 물리적 서버를 통합한다.)

> Host Os와 Guest OS

#### Host Os

하드웨어 위에 설치된 운영체제를 의미.

#### Guest OS

호스트 가상화 혹은 하이퍼바이저 위에 설치된 운영 체제. (리눅스, 윈도우 등)

> 가상화 종류

|구분 |특징|
|:----|:----:|
| 호스트 가상화  |  Host Os 위에 Guest OS가 실행되는 방식.(VMServer, Virtual Box, VM Workstation 등)  |
| 하이퍼바이저  |  Host Os가 없음. 하이퍼바이저 위에 Guest OS. (Xen, Microsoft Hyper-V, Citrix, KVM 등)  |
| 컨테이너 가상화 |  Host OS 위에 컨테이너 관리 소프트웨어를 설치하여 논리적인 컨테이너를 나누어서 사용한다. (Docker) |  



> 하이퍼 바이저(Hyper Visor)

하드웨어 위에 별도의 Host OS를 설치하지 않고 하이퍼바이저라는 가상화 소프트웨어를 설치한다. 그리고 하이퍼바이저 위에 Guest OS를 설치하는 구조.

> 하이퍼바이저 가상화의 종류

|수준 |Type-1(Native, Bare metal) |Type-2(Hosted)|
|:----|:----|:----:|
|네번째|   |  GuestOS  |
|세번째|GuestOS   |  하이퍼바이저  | 
|두번째|하이퍼바이저|HostOS| 
|첫번째|하드웨어   |  하드웨어  | 

> 하이퍼바이저 가상화의 장단점

- 장점 :  Host OS가 없기 때문에 오버헤드가 적다. 

  ( 오버헤드 : 처리를 하기위해 들어가는 간접적 처리시간/메모리 )
- 단점 : 자체적으로 머신에 대한 관리 기능이 없기 때문에 관리를 위한 컴퓨터 혹은 콘솔이 필요.


### On-Premise
서버, 데이터베이스, 네트워크 등의 장비를 모두 구매후, 구축하고 운영하는 서비스.
일반적으로 IDC에 서버를 설치하고 전용 네트워크를 통해서 운영하는 시스템 형태.

> IDC(Internet Data Center)

- 서버랙 : 랙은 서버를 설치하는 장치를 의미.
- 케이블 타워 : 각종 서버에 케이블 연결하여 통신, 케이블은 케이블 타워에 설치.
- 항온항습기 : 온도 습도 조절


### 클라우드 컴퓨팅 종류
서비스를 제공하는 방식에 따라 분류함.
- Private Cloud : 기업 내부에서 기업 조직원들을 위한 서비스 제공. 
- Public Cloud : 인터넷을 사용해서 제공하는 클라우드 컴퓨팅. (AWS, AZURE 등)
- Hybrid Cloud : private Cloud, Public Cloud 모두 제공.

### 클라우드 컴퓨팅 모델

#### 1. IaaS(Infrastrucure as a Service)
- 인프라를 서비스 형태로 제공. *서버, 스토리지, 네트워크 관련* 각종 *물리적 장비*를 서비스 형태로 제공.
- AWS에서 EC2, S3, VPC 등의 서비스가 해당된다.
#### 2. PaaS(Platform as a Service)
- 인프라에 설치되는 *운영체제, 미들웨어, 데이터베이스 관리 시스템* 등의 *소프트웨어*를 제공.
- AWS에서 리눅스 및 윈도 운영체제, Oracle, MySQL 등의 DBMS를 제공하는 것.
#### 3. SaaS(Software as a Service)
- *응용 프로그램*(구글 Office 365, 드롭박스 등)을 서비스 형태로 제공.


## [spring boot]

### AdminUserController에서 User 객체를 이용해 멤버를 하나하나 복사해 와서 adminUser를 통해 전체 조회하는 예제를 실행해봄.

여기서 MappingJacksonValue 클래스가 어떤건지에 대해서 궁금해져서 알아보았다.

> MappingJacksonValue란?

MappingJacksonValue는 JSON Serialization(직렬화)을 처리하는 데 사용되며, 주로 Spring MVC(혹은 Spring  WebFlux) 기반의 웹 애플리케이션에서 Java 객체를 JSON으로 변환하거나, 반대로 JSON 데이터를 Java 객체로 변환하는 데 매우 효율적이고 강력한 라이브러리. 
 
일반적으로 컨트롤러 메서드에서 반환되는 데이터를 래핑하는데 사용되며, 이를 통해 특정 필터링 기능이나 직렬(Serialization) 설정을 적용하여 응답 데이터를 제어할 수 있습니다.


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
여기서부터는 URI를 통한 접근이 불가능하고, POSTMAN에 있는 header 기능을 이용하여 호출한다.
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
		3. headers 버전관리		(예시 사이트 : Microsoft)
		4. mime-type 버전관리		(예시 사이트 : GitHub)

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





## 05/22
### AWS(Amazon Web Service)
컴퓨팅, 네트워킹, 스토리지, 분석 플랫폼 등 다양한 서비스를 제공.

> 컴퓨팅 서비스

- Amazon EC2 : 다양한 타입의 가상화 서버(Windows, Linux, Aurora)를 지원.
- Amazon Auto Scaling : 사용량에 따른 자동 서버 추가 삭제
- Amazon Lightsail : VPS(Virtual Private Server)는 웹사이트 및 웹 어플리케이션을 배포하거나 관리.
- Amazon Workspace : 데스크톱 가상화 서비스. (사내PC는 가상화), (개인 PC는 문서를 서버에 보관. 저장x)

> 네트워킹 서비스

|서비스 |설명|
|:----|:----:|
| Amazon Route 53  |  클라우드 기반의 DNS(Domain Name System)  |
| Amazon VPN  |  가상 사설 네트워크를 구성(DHCP, VPN 사용)  |
| AWS Direct Connect | AWS를 연결하기 위해서 전용선을 구성하는 것. (AWS-ON-Premise를 연결)  |  
| Amazon ELB(Elastic Load Balancer) | 네트워크 부하를 분산하기 위해서 L4 스위치 역할  | 

- L4스위치 : 서버가 점점 늘어나다보면 네트워크에 부하가 가게 된다. 이때 필요한 것이 로드밸런싱(서버 부하 분산)이다. 외부에서 들어오는 모든 요청을 서버가 아닌 L4 스위치가 받아 서버들에게 적절히 나누어 준다.


> 스토리지 서비스

|서비스 |설명|
|:----|:----:|
| Amazon S3  |  클라우드 기반의 DNS(Domain Name System)  |
| Amazon DynamoDB  |  NoSQL 서비스로 대용량의 데이터를 저장,분석  |
| Amazon ElasticCache | In-memory 기반의 Cache 서비스.  | 


> AWS CloudWatch 서비스

자원과 성능을 모니터링하고 통지하는 서비스

### AWS 장점
1. 사업 초기 투자비용이 발생하지 않는다.
	- 사업을 하기 위해서 정보시스템이 필요.
	- 정보시스템 구축을 위해서 시설이 필요
	- 하지만 AWS는 이 모든 시설을 구축해서 제공하고 있음
	- 따라서 *인건비, 운영비용 감소효과*
2. 탄력적 확장이 가능하다. -> 속도, 민첩성
	- 저렴한 서버를 구매함.
	- 사용자가 폭증.
	- 다시 서버를 구매해야함.
	- 하지만 AWS는 서비스 형태로 제공되므로 바로 확장 가능.
	- -> 사용자는 본인 사업에 집중할 수 있다.
3. 전 세계로 확장이 가능.


## [GCP]

### 클라우드란

- On-Premises : ( 집을 지을때 자재부터 직접 사서 지음 )하드웨어부터 애플리케이션, 확장까지 모든것을 직접 설치해 구동시키는것. 

- IaaS : ( 깡통 집은 지어줌 )운영체제, 런타임, 확장 등에 대해서는 사용자가 직접 관리해야함.
- CaaS : ( 집을 임대한다. + 기본적인 설비 but 가구는 없다 ) 컨테이너 화된 어플리케이션은 설치가능 but 확장과 런타임에 대해서는 관리가 필요.
- PaaS : ( 가구까지 제공하는 집 임대 ) 자체 코드를 가져와 배포하지만 확장은 공급자에게 맡길 수 있다.

- FaaS : ( 사무실 임대 ) 함수 또는 코드 일부를 배포, 해당 함수 실행될 때마다 클라우드 공급자는 필요에 따라 규모를 확장

- SaaS : ( 청소나 잔디 유지비용 지불 ) 비용을 지불하면 업체가 데이터를 관리 해 준다.

### Compute Engine
맞춤형 컴퓨팅 서비스, 일반 사용자가 구글 인프라 상에서 가상 머신(VM)을 구동 할 수 있다.

1. 사전 정의된 머신 유형(predefined machine type)
	- vCPU와 메모리를 가진 VM구성
	- 사전에 생성돼 빠르게 사용할 수 있다.
2. 사용자 정의형 머신 유형(custom machine type)
	- 작업 부하에 따라 최적의 CPU와 메모리를 가진 vm 생성가능
	- 작업 부하에 맞게 인프라 조정
	- 요구사항 변경 -> 더 작거나 큰 머신 유형 인스턴스 또는 사전에 정의된 구성으로 작업 이전 가능.

### 머신유형
작업 부하에 따라 제품군으로 분류됨.

1. 일반목적
	- 비용이 저렴 -> 일상적 컴퓨팅
	- 균형잡힌 가격과 성능

2. 컴퓨팅 최적화
	- *최고성능*을 요구하는 작업에 권장
	- 게임, 비디오, 전자 설계 등
3. 메모리 최적화
	- 큰 메모리 작업, 내장 메모리 분석에 권장
4. 가속기 최적화
	- 고성능 요구 작업
	- 대규모 계산, 머신러닝


## [spring boot]
### Swagger Documentation 구현
|Swagger 3 annotations |Description|
|:----|:----:|
| @Tag  |  클래스에 설명, Swagger 리소스  |
| @Parameter  |  API 에서의 단일 매개 변수  |
| @Parameters | API 에서의 복수 매개 변수  | 
| @Schema | Swagger모델에 대한 추가 정보  | 
| @Operation(summary="",description="") | 특정 경로에 대한 작업   | 
| @ApiResponse(responseCoded="404",description="") | API에서의 작업 처리에 대한 응답코드 설명  | 


### Swagger 들어가는법
http://localhost:8088/swagger-ui/index.html#/

여기로 들어가면 됨.

## 05/23
### [ SQL 문제풀기 - HackerRank ]
새벽에 자기전 한문제 풀고 잔다
- 문제 : CITY 테이블에서 POPULATION이 100000보다 크고, COUNTRYCODE가 USA인 모든 쿼리를 출력하라.
- 답 : 
```
select *
from CITY
where population > 100000 and countrycode = 'USA'
```
- 결과 : 정답

### [nginx 설치]
프로젝트 배포를 위해 미리 다운로드를 해 보았다. 여러가지 문제가 있어서 해결하는데 오래걸렸고, 해결과정을 티스토리 블로그에 올렸다.

### [spring boot]

- Actuature을 이용해서 모니터링과 Metrics를 수집함.
	1. yml 파일에
	```
	management:
  		endpoints:
    		web:
      			exposure:
        		include: "*"
	```
	를 추가 하면 include 안에 정의한 정보들이 보여지게 된다.
	
	모든 정보들을 다 보이고 싶으면 include : * 하면 되지만,
몇가지만 공개하고 싶다면 include : "self, health" 와 같이 입력하면 됨.


	예)

	http://localhost:8088/actuator/metrics 는 어떤 메트릭스를 사용하는지 메모리가 얼마나 남았는지 같은 수치정보를 볼 수 있다.

	http://localhost:8088/actuator/beans 는 현재 어떤 bean이 등록되어 있는지 볼 수 있다.

- HAL Explorer를 이용한 API 테스트
	- HAL Explorer
	```
	1. HAL은 API 리소스들 사이에서 필요로 하는 일괄적인 하이퍼링크를 제공하는 방식. 
	API를 설계할때 HAL을 사용하게 됨으로써 API간에 쉽게 검색이 가능하다.
	2. response 정보에 부가적인 정보를 서비스해줄 수 있다.
	3. rest 자원을 표시하기 위한 자료를 그때그때 사용하지 않더라도 해태우스 기능을 바로 연결해서 쓸 수 있다.
	```


	http://localhost:8088/explorer/index.html#uri=/actuator

	이걸로 들어가면 json 형식으로 나왔던 코드들이 깔끔하게 페이지에 나온다.


- Spring Security를 이용한 인증 처리
	1. pom.xml에 추가
	```
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-security</artifactId>
	</dependency>
	```
	2. 구동시킬때 나오는 비밀번호로 postman에서 password 입력하면 됨.

	![Alt text](<spring 4_9.png>)

- API 사용을 위한 사용자 인증 처리 구현 (2가지의 방법이 있다.)
	1. application.yml에 security 추가
	```
	spring:
 	 	message:
 	  		 basename: messages
		security:
   			 user:
  	    		name: username
     	 		password: passw0rd
	```

	2. 인코딩으로 처리하는 방법
	```
	BCryptPasswordEncoder 사용 BCryptPasswordEncoder는 crypt 해싱함수를 사용한다.
	사용자 비밀번호를 인코딩해주는 메소드와, 입력한 비밀번호와 저장된 비밀번호가 일치하는지 확인할 수 있는 메소드를 제공해준다.
	해싱하고자 하는 강도(?) 도 조정할 수 있게 해준다.
	```
	1번을 주석처리하고 config 패키지에 SecurityConfig 클래스를 만든다.
	BCryptPasswordEncoder를 등록하고, 이를 통해 비밀번호의 보안에 적용시킨다.
	


### [ SQL 문제풀기 - HackerRank ]
3문제 풀었다.


### [ 학습의 3단계 ]
인프런 소개 영상을 듣다가 학습의 3단계라는 것을 배웠다.

> 1단계 : 학습

말 그대로 강의를 듣거나, 책을 읽거나 하는 배우는 것.

> 2단계 : 체득

내가 실제로 기능들을 따라 쳐보면서 체득하는것.

강의를 다 듣고 토이프로젝트를 진행하는 것을 추천!

> 3단계 : 정리

실제로 내가 배운것을 다른사람에게 설명할 수 있을 정도의 단계가 되는것.

-------------------------
--------------------
사실 머리로는 알고 있지만 이렇게 정리해보니 더 머리에 잘 들어왔다.

나는 현재 듣고 있는 강의를 듣고(학습), 간단한 rest api 토이프로젝트를 만들것이다.(체득) 그리고 그 과정들에 대한 나만의 고찰과 방식들을 블로그에 소개해보고싶다.(정리)


## 05/24

### [spring boot]

### ORM (object relational mapping)
- 객체를 관계형 데이터 베이스에 있는 데이터오 자동으로 매핑해주는 기능
- sql 문장을 자동으로 생성가능

### JPA (Java Persistence API)
- 관계형 데이터베이스를 사용하기위한 방식을 정의해 놓은 인터페이스 -> 특정 기능을 사용할 수 있는 라이브러리가 아니다
- 자바 ORM 기술에 대한 API 표준 명세서 (단순한 명세서) -> 구현되어있는 메소드가 없다. -> JPA를 구현한 구현체가 필요 -> Hibernate

### Hibernate
- 생산성, 유지보수, 비종속성
- ORM 기술을 위한 라이브러리 AND JPA와 같은 인터페이스의 구현 클래스들의 집합체

### Spring Data JPA
- 스프링 모드 중 하나
- JPA를 추상화한 Repositorty 인터페이스 제공
- crud를 편하게 개발하도록 crud의 공통적인 인터페이스 제공

### 자바에서는 아래에서 위 순서로 추상화 되어있다.
|JAVA |
|:----|
| Spring Data  |
| JPA  | 
| Hibernate |
| JDBC |


### JPA 사용을 위한 Dependency 추가와 Entity 설정
> H2 데이터베이스를 사용

1. h2 web console 주소 : localhost:8088/h2-console
2. 야물파일 수정

	```
	spring:
		message:
			basename: messages
		datasource:
			url: jdbc:h2:mem:testdb
			username: sa
		jpa:
			show-sql: true                          # 작업되고 있는 sql문장도 로고파일에 보일 수 있도록
			hibernate:
				ddl-auto: create-drop               # 나중에 데이터베이스 관련작업에 필요
			generate-ddl: true
			defer-datasource-initialization: true   # 스크립트 파일(저장하고 싶은 데이터만 모아저있는 파일)이 있을경우,
													# 하이버네이트 초기화 이후에 바로 작동할 수 있도록 설정.
		h2:
			console:
				enabled: true                       # 사용가능하도록
				settings:
					web-allow-others: true          # 웹 페이지에서 콘솔을 사용할 수 있도록 제공
	```

> 테이블 생성

- h2 연결하고 (jpa가 매핑시켜준것임)
- user클래스에 @Entity라는 어노테이션을 적용해준다.
- user라는 클래스 이름으로써 데이터베이스 테이블이 생성됨 -> 인스턴스들로 컬럼구성
- 기본키로 적용시키고 싶은 인스턴스 위에 @Id라고 적으면 기본키가 됨
- 그 밑에 @GeneratedValue를 적으면 "이 값은 자동으로 생성되는 값입니다." 라는 의미가 됨.
- @Table(name = "users") 라고 적으면 테이블 이름이 users로 변경됨.

-> h2 사이트에서 나갔다가 다시 연결하면 테이블이 생성된 것을 확인 할 수 있다.

### Spring Data JPA를 이용한 초기 데이터 생성

- Spring Data JPA를 이용한 초기 데이터 생성


### JPA Service 구현을 위한 Controller, Repository 생성
- 새로운 패키지 생성(repository)
- 그 안에 UserRepository 인터페이스를 만들고 JpaRepository 인터페이스를 상속한다.

### JPA를 이용한 개별 사용자 상세 조회 - HTTP Get method
- id 값을 uri에 추가해서 한 명의 정보만 받아오기!

### JPA를 이용한 사용자 추가와 삭제 - HTTP POST/DELETE method
- update, delete 기능들은 그냥 작동되지 않는다. security를 해야한다. -> securityconfig로 이동


## 05/26

### [ SQL 문제풀기 - HackerRank ]
- CITY 테이블에서 COUNTRYCODE가 JPN인 모든 정보를 가져와라.
- CITY 테이블에서 COUNTRYCODE가 JPN인 이름 정보를 가져와라.
- STATION 테이블에서 CITY 와 STATE 정보를 가져와라.
- STATION 테이블에서 CITY 와 ID 정보를 가져와라. (단, 중복정보는 제외하고 ID번호는 짝수)
	- 짝수 홀수 구하는 방법을 까먹었다...
	- 짝수 : MOD(컬럼명, 2) = 0
	- 홀수 : MOD(컬럼명, 2) = 1

## 05/27


### [ SQL 문제풀기 - HackerRank ]

- STATION 테이블에서 CITY 컬럼의 전체 항목 수와 중복되지않는 CITY의 차를 구해라.
	- count와 distinct를 쓰는것이 관건
- 가장 길고 가장 짧은 CITY를 출력. 가장 짧거나 가장 긴 이름의 CITY가 두 개 이상인 경우 알파벳 순으로 먼저나온 CITY를 선택해라.
	- 간만에 까다로웠던 문제
	```c#
	select *
	from
	(
		select city, length(city) // 문자열 길이
		from station
		where length(city) = (select min(length(city)) from station) // 가장 길이가 긴 city 찾기
		order by city asc
	)
	where rownum = 1;		// 첫 행만 나오도록

	select *
	from
	(
		select city ,length(city) // 문자열 길이
		from station
		where length(city) = (select min(length(city)) from station) // 가장 길이가 짧은 city 찾기
		where length(city) = (select max(length(city)) from station)
		order by city asc
	)
	where rownum = 1;		// 첫 행만 나오도록

	```
<br>



### [spring boot]
<br>

- 게시물 관리를 위한 Post Entity 추가와 초기 데이터 생성
	> @Entity

	@Entity 어노테이션을 달면, jpa에서 해당하는 클래스를읽어들이고 이 정보를 토대로 db를 생성.
	<br><br>


	> User와 Post는 1:N의 관계성을 가진다.
		
		1. user 한 명이 게시물 여러개 작성 가능
		2. user 한 명이 게시물 0개 작성 가능

		3. user가 없는데 게시물 존재 불가능
		4. 여러명의 user가 하나의 게시물 작성 불가능
	<br>

	> @OneToMany

	User 클래스에 @OneToMany(mappedBy = "One(맨앞) 이 누구냐")

	<br>

	> @ManyToOne

	Post 클래스에 @ManyToOne(fetch = FetchType.LAZY)

	LAZY는 지연로딩 : post 데이터가 사용자 데이터를 조회할때 매번 post데이터를 즉시 가져오는 것이 아니라 post가 로딩되는 시점에.
	즉, 필요한 시점에 즉시 가져오기위함.

	원래 jpa에서 연관관계에 있는 엔티티들은 즉시 로딩을 하기 위해서 EAGER라는 옵션으로 되어있는데, getposts()라는 요청을 하게 됐을때, 그때 사용되는 시점에 post의 엔티티들을 가져올 수 있끔 로딩 방식을 천천히 가져오겠다. 라는 뜻이다.

	<br>

	> @OneToMany

	@OneToMany 는 부모와 자식테이블에도 사용할 수있다.
	<br><br>
	부모테이블은 @OneToMany<br>
	자식테이블은 @ManyToOne 을 쓰는게 일반적



### 과제 해결하는 과정
https://hyeonic.tistory.com/197

ResponseEntity 공부하기

<br><br>

## 05/28

### [ SQL 문제풀기 - HackerRank ]

- STATION 테이블에서 a,e,i,o,u 로 시작하는 CITY를 출력해라.
	- in 연산자를 사용. 값이 계속 안나오길래 뭐지? 생각했는데, 대문자 A,E,I,O,U로 하니 값이 제대로 나왔다.







		
