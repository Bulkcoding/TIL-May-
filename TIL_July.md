## 07/01
### [ SQL 문제풀기 - HackerRank ]
```
1. 받은 점수별로 grade가 매겨진다.(0~9는 1grade...90~100은 10grade)
2. grde가 8 미만이면 이름에 null 출력.
3. students 테이블과 Grades 테이블이 주어진다.
4. grade 순으로 내림차순 정렬
5. 점수가 높은 사람이 제일 위로 가도록 출력.
6. 이름이 null인 같은 등급의 학생들은 점수를 오름차순으로 정렬.
```

<br>

case 문으로 이름을 Null로 만드는것은 예상했으나, order 문에도 사용할 수 있는지는 몰랐다.

특히, -S.marks ASC는 S.marks DESC와 같다는 것을 알고 넘어가야 할 것 같다. 

<br>

```SQL
select case when G.grade < 8 then NULL else S.Name end as Name,
G.grade,
S.marks
from Students S join Grades G
On G.Min_Mark = trunc(S.marks,-1) or G.Max_Mark= trunc(S.marks,-1)
order by G.grade desc,Name asc,
CASE 
        WHEN G.grade < 8 THEN S.marks 
        ELSE -S.marks 
    END ASC;
```

<br>

### [ 정처기 이론 - 이론 ]
- 소프트웨어 생명주기
- 프로젝트 계획
- 요구사항 분석
- 소프트웨어 설계
- 소프트웨어 구현

를 학습하였다.

<br>
<br>

## 07/02
### [ SQL 문제풀기 - HackerRank ]
```
1. 둘 이상의 챌린지에서 만점을 받은 학생의 id와 이름을 출력하라.
2. 만점받은 총 수에 따라 내림차순으로 정렬하고, id로 오름차순하라.
```
- 만점을 가장 많이 받은 학생을 출력하는걸로 잘못 해석해서 오래걸렸다.

<br>

```sql
SELECT H.hacker_id, H.name
FROM Hackers H JOIN Submissions S ON H.hacker_id=S.hacker_id JOIN Challenges C ON S.challenge_id=C.challenge_id JOIN Difficulty D ON C.difficulty_level=D.difficulty_level
WHERE S.score=D.score
GROUP BY H.hacker_id, H.name
HAVING COUNT(C.challenge_id)>1
ORDER BY COUNT(C.challenge_id) DESC, H.hacker_id;
```
- group by 절의 조건식인 having을 써서 둘 이상 만점받은 학생을 가려냈다. 

<br>

### [ 정처기 이론 - 이론 ]
- 소프트웨어 테스트
- 소프트웨어 유지 보수
- 데이터베이스
    - 스키마
    - 데이터베이스 설계 순서
    - 개체-관계 모델
    - 키 (Key)
    - 무결성
    - 정규화


<br>
<br>

## 07/03
### [ SQL 문제풀기 - HackerRank ]
```
1. wands 테이블과 wands_property 테이블이 주어진다.
2. wands : id, power, coins_needed  /  wands_property : age  출력
3. power 내림차순 정렬 출력, age 내림차순
4. age와 power가 높고, is_evil과 coins_needed가 낮은것을 골라라
```

<br>

```sql
SELECT W.id, WP.age, W.coins_needed, W.power 
FROM Wands W INNER JOIN Wands_Property WP ON W.code=WP.code 
WHERE 
((W.coins_needed, W.power, WP.age) IN 
 (SELECT MIN(W.coins_needed) AS coins_needed, W.power, WP.age
  FROM Wands W INNER JOIN Wands_Property WP ON W.code=WP.code
  GROUP BY W.power, WP.age)
) 
AND 
(is_evil=0) 
ORDER BY W.power DESC, WP.age DESC;
```
where 절이 point이다. power와 age로 그룹을 만들고, coins_needed의 최솟값을 가져온 값들을 조건에 넣는다. evil은 0부터 값이 존재하므로 0인 것들만 가져왔다.

<br>

### [ 정처기 이론 - 이론 ]
- 데이터베이스
    - 함수적 종속
    - 관계대수
    - 관계 해석
    - 트랜잭션
    - 데이터 회복 기법
    - 로킹 단위
    - 분산 데이터베이스
    - 알고리즘
- 운영체제
    - 종류
    - UNIX 구성요소

<br>
<br>

## 07/04
### [ 정처기 이론 - 이론 ]
- 운영체제
    - 기억장치 / 메모리
    - 페이지 분할기업
    - 페이지 교체 알고리즘
    - 프로세스와 스레드
    - 스케쥴링
    - 교착상태
- 네트워크
    - 정보 전송 방식
    - 프로토콜
    - OSI 7계층
    - 네트워크 프로토콜


<br>
<br>

## 07/05
### [ SQL 문제풀기 - HackerRank ]
```
1. hackers 테이블의 hacker_id, name과 challenges 테이블의 과제의 총 개수 출력를 출력하라.
2. 총 개수를 내림차순하여 정렬하고, 총 개수가 같을경우 hacker_id로 정렬하라.
3. 총 개수가 중복된 경우 max(과제수) 보다 작으면 출력x, max(과제수)에 맞으면 출력.
```


<br>

```sql
with a as (
    select hacker_id, count(*) as counts
    from challenges
    group by hacker_id
)
select a.hacker_id, name, a.counts
from a
join hackers h on h.hacker_id = a.hacker_id
where a.counts not in (select counts
                                    from a
                                    group by counts
                                    having count(*) > 1 and counts < (select max(counts) from a)
                                    )
order by counts desc, hacker_id;
```


<br>
<br>

## 07/06
### [ 정처기 이론 - 이론 ]
- 네트워크
    - 전송, 응용 계층 프로토콜
    - IP 헤더 구조
    - TCP 헤더 구조
    - 패킷 교환 방식
    - 라우팅
    - VPN 관련 프로토콜
    - IP 주소 체계
- 정보 보안
    - 보안의 3대 요소
    - 양방향 암호화와 단방향 암호화 방식
    - 서비스 공격 유형
    - 정보 보안 솔루션
    - 정보 보안 프로토콜
    - 코드 오류
    - 정보 보안 침해 공격
- 기타 용어
    - 웹 서비스
    - 인터페이스 구현
    - 트리 순회 방법
    - 클라우드 서비스
    - RAID
    - 디지털 저작권 관리
    - IT 용어

<br>
<br>

## 07/07
### [ JAVA 문제풀기 - HackerRank ]
> scan 이용시 런타임 오류를 제거하려면

nextLine()으로 문자열을 입력으로 받을 때 Enter 키를 누르자마자 입력을 기다리지 않고 빈 줄을 입력으로 받습니다. 따라서 nextLine()으로 입력을 받을 때는 항상 nextInt() 또는 nextDouble() 뒤에 nextLine()을 추가로 넣어야 한다.

```java
public static void main(String[] args) {
    Scanner scan = new Scanner(System.in);

    int i = scan.nextInt();         
    double d = scan.nextDouble();
    scan.nextLine();
    String s = scan.nextLine();         
    
    System.out.println("String: " + s);
    System.out.println("Double: " + d);
    System.out.println("Int: " + i);
}
```

<br>


### [ 정처기 이론 - 기출문제 ]
- 형상관리
    - 절차
- 디자인 패턴
- 화이트박스, 블랙박스 테스트 기법
- 애플리케이션 테스트 유형 분류

<br>
<br>

## 07/08
### [ 정처기 이론 - 기출문제 ]
- 프로세스, 프로그램, 프로세서
- 단편화, 페이징, 세그멘테이션
- 주기억장치
    - 반입
    - 배치
    - 교체
- 스레싱
- 기아현상
- 네트워크 계산 문제 
