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

### [ 정처기 이론 ]
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

### [ 정처기 이론 ]
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

### [ 정처기 이론 ]
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
### [ 정처기 이론 ]
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
### [ 정처기 이론 ]
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
- 관계대수, 관계해석

<br>

### [ JAVA 문제풀기 - HackerRank ]
- 문자와 숫자를 받아서 자리수 채우기

> 두 가지 방법이 있다

1. String.format 이용하기
    - String.format("%05d", 숫자);
    - 숫자를 포함해서 5자리를 차지하는데 빈공간은 0으로 채워라
    - 반대로 하려면 -05d

2. String.Utils 라이브러리 이용하기
    - StringUtils.leftPad(문자열, 5, "_");
    - _ 로 5자리 맞추기


<br>
<br>

## 07/09
### [ JAVA 문제풀기 - HackerRank ]
- 루프문을 통해 숫자를 받아 구구단 만들기

<br>

### [ 정처기 이론 - 기출문제 ]
- 공개키 암호 알고리즘
- 단방향 암호 알고리즘
- 라우팅 프로토콜
- 인수 테스트
- Regression(회귀 테스트)
- 테스트의 기본 원칙
    - 파레토의 법칙
    - 살충제 패러독스
- 객체지향 설계원칙 (SOLID)
    - 단일 책임원칙
    - 개방폐쇄원칙
    - 리스코프 치환 원칙
    - 인터페이스 분리원칙
    - 의존성 역전 원칙

<br>
<br>

## 07/10
### [ 정처기 이론 - 기출문제 ]
- 함수종속
- 로그기반 회복기법
- 트랜잭션의 특성 (AICD)
- 이상현상
- UI 설계원칙
- UI 종류
- 정적분석, 동적분석
- 유닛 테스트 : JUnit
- 애플리케이션 테스트 유형
- 데이터베이스 Key 종류와 특징
- 무결성 제약조건

<br>

### [ cs 공부 ]
디자인패턴(목적, 특징, 원칙)에 대해 알아보고, 생성, 구조, 행위 패턴에 대해 공부함.

<br>
<br>

## 07/11
### [ JAVA 문제풀기 - HackerRank ]
- 등차수열의 합에 관한 로직 풀기

### [ 정처기 - 프로그래밍언어 ]
- 프로그래밍 언어(java)복습

<br>
<br>

## 07/12
### [ SQL 문제풀기 - HackerRank ]
```
hackers테이블과 Submissions테이블이 있다. 
1. hacker_id, name, 총점을 내림차순으로 정렬한다.
2. 두명 이상의 해커가 같은 총점을 달성한 경우 hacker_id를 오름차순으로 정렬하라.
3. 총점이 0인 해커는 출력하지 않는다.
```
<br>

```sql
with v as (
    Select h.hacker_id, h.name, s.challenge_id, max(s.score) as score
    from Submissions S join hackers H on S.hacker_id = H.hacker_id
    group by h.hacker_id, h.name, s.challenge_id
    order by h.hacker_id
)
select v.hacker_id, v.name, sum(v.score)
from v
where v.score >0
group by v.hacker_id, v.name
order by sum(v.score) desc, v.hacker_id asc;
```
전부 짜놨는데, oerder by 가 문제였다.
나는 order by 문에서 case문을 활용하여 count가 1보다 큰 경우를 찾아내 오름차순을 하려고 했지만, 쉽지 않았다.
결국 다른 사람의 코드를 참조해서 알아냈는데,

일단 총점으로 내림차순하고 hacker_id로 오름차순하면 일단 같은 총점끼리는 정렬이 되니까 두명이상인지 한눈에 볼 수 있고, 그 상태에서 hacker_id로 오름차순 정렬하면 되는것이었다.

문제에서 hacker_id, name, 총점을 정렬하라고 했는데, hacker_id, name, 총점 desc가 먼저 나와야하는거 아닐까...?

정렬하라는 문제는 뭐가 정답인지 몰라서 까다로운것 같다.

<br>
<br>

## 07/13
### [ SQL 문제풀기 - HackerRank ]
```
start_date  end_date
2015-10-01 2015-10-02
2015-10-02 2015-10-03
2015-10-03 2015-10-04
2015-10-04 2015-10-05
2015-10-11 2015-10-12
2015-10-12 2015-10-13

와 같은 데이터가 저장 되어 있는 테이블인 경우
end_date와 다음행의 start_date가 같은 경우 end_date는 계속 다음행의 end_date가 된다.

예)
start_date  end_date
2015-10-01 2015-10-05
2015-10-11 2015-10-13
```
<br>

> 1단계



```sql
    SELECT 
        start_date,
        end_date,
        CASE 
            WHEN end_date - LAG(end_date) OVER (ORDER BY end_date) > 1 THEN 1 
            ELSE 0 
        END AS diff
    FROM Projects

```

이 테이블을 실행하면


```
2015-10-01 2015-10-02 0
2015-10-02 2015-10-03 0
2015-10-03 2015-10-04 0
2015-10-04 2015-10-05 0
2015-10-11 2015-10-12 1
2015-10-12 2015-10-13 0
2015-10-15 2015-10-16 1
2015-10-17 2015-10-18 1
2015-10-19 2015-10-20 1
2015-10-21 2015-10-22 1
2015-10-25 2015-10-26 1
2015-10-26 2015-10-27 0
```

이런 데이터가 나온다. 그럼 0과 1로 섹션이 나눠진다.

<br>

> 2단계

```sql
WITH Add_date_diff AS (
    SELECT 
        start_date,
        end_date,
        CASE 
            WHEN end_date - LAG(end_date) OVER (ORDER BY end_date) > 1 THEN 1 
            ELSE 0 
        END AS diff
    FROM Projects
)
    SELECT 
        start_date,
        end_date,
        SUM(diff) OVER (ORDER BY end_date) AS project_num
    FROM Add_date_diff
```
이렇게 짜게 되면 해당하는 항목별로 0부터 차례대로 번호를 받게된다.

```
2015-10-01 2015-10-02 0
2015-10-02 2015-10-03 0
2015-10-03 2015-10-04 0
2015-10-04 2015-10-05 0
2015-10-11 2015-10-12 1
2015-10-12 2015-10-13 1
2015-10-15 2015-10-16 2
2015-10-17 2015-10-18 3
2015-10-19 2015-10-20 4
2015-10-21 2015-10-22 5
```

<br>

> 3단계

```sql
WITH Add_date_diff AS (
    SELECT 
        start_date,
        end_date,
        CASE 
            WHEN end_date - LAG(end_date) OVER (ORDER BY end_date) > 1 THEN 1 
            ELSE 0 
        END AS diff
    FROM Projects
),
Add_project_num AS (
    SELECT 
        start_date,
        end_date,
        SUM(diff) OVER (ORDER BY end_date) AS project_num
    FROM Add_date_diff
)
SELECT 
    MIN(start_date) AS min_start_date, 
    MAX(end_date) AS max_end_date
FROM Add_project_num
GROUP BY project_num
ORDER BY COUNT(*), MIN(start_date);
```

번호대로 그룹을 묶은 상태로 start_date는 최솟값을, end_date는 최댓값을 가지면 원하는 결과값을 얻을 수 있다.

```
2015-10-15 2015-10-16
2015-10-17 2015-10-18
2015-10-19 2015-10-20
2015-10-21 2015-10-22
2015-11-01 2015-11-02
2015-11-17 2015-11-18
2015-10-11 2015-10-13
2015-11-11 2015-11-13
2015-10-01 2015-10-05
2015-11-04 2015-11-08
2015-10-25 2015-10-31
```
<br>

이번 쿼리도 내 힘으로 풀진 못했다. 기껏해야 LAG,LEAD를 써야할것 같다는것 정도가 한계였다. 이 단계부터는 쿼리를 이해하는 것을 목표로 해야겠다.

<br>
<br>

## 07/14
### [ JAVA 문제풀기 - HackerRank ]
- byte,short,int,long의 범위관련 문제
- long같은경우 범위가
```java
if(x>=-9223372036854775808L && x <= 9223372036854775807L)
```
숫자가 큰 경우 끝에 L을 꼭 붙여줘야 한다.

<br>

### [ 정처기 - 프로그래밍언어 ]
- Java
    - 메서드 오버라이딩
    - 메서드 오버로딩
    - 메서드 하이딩
    - 예외처리

<br>

### [ 정처기 이론 - 기출문제 ]
- 테스트의 목적
    - 회복
    - 안전
    - 강도
    - 성능
    - 구조
    - 회귀
    - 병행
    - A/B테스트
    - 스모크 테스트

### [ cs 공부 ]
디자인패턴 중 MVC, MVP, MVVM에 대해 공부함.

<br>
<br>

## 07/15
### [ JAVA 문제풀기 - HackerRank ]
- Scanner.hasNext() 메소드를 통해 문제 풀기.
```java
[input 내용]
Hello world
I am a file
Read me until end-of-file.

[output 해야할 내용]
1 Hello world
2 I am a file
3 Read me until end-of-file.
```

<br>

```java
public static void main(String[] args) {
    
    String a;
    int b = 1;
    Scanner scanner = new Scanner(System.in);
    while(scanner.hasNext()){
        a = scanner.nextLine();
        
        System.out.println(b+" "+a);
        b++;
    } 
}
```
scanner.hasNext()로 값이 비어있을때만 while문이 돌아가도록 한다.

<br>

### [ 정처기 - 프로그래밍언어 ] - 복습
 

<br>

### [ 정처기 이론 - 기출문제 ] - 복습


<br>
<br>

## 07/16
### [ JAVA 알고리즘() 문제풀기 - HackerRank ]
```
6               arr[] size n = 6
-4 3 -9 0 4 1   arr = [-4, 3, -9, 0, 4, 1]
```
이렇게 input값이 들어오면
size 개수로 (양수개수, 음수개수, 0의 개수)를 나눈 값을 소수점 6자리로 나타내라.


```java
class Result {

    public static void plusMinus(List<Integer> arr, int n) {
    
        int count0 = 0;
        int countP = 0;
        int countM = 0;
    
        for(int num:arr){
            if(num == 0) count0++;
            if(num < 0) countM++;
            if(num > 0) countP++;
        }
        
        System.out.println(String.format("%.6f",(double)countP/n));
        System.out.println(String.format("%.6f",(double)countM/n));
        System.out.println(String.format("%.6f",(double)count0/n));
        
    }
}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));

        int n = Integer.parseInt(bufferedReader.readLine().trim());

        List<Integer> arr = Stream.of(bufferedReader.readLine().replaceAll("\\s+$", "").split(" "))
            .map(Integer::parseInt)
            .collect(toList());

        Result.plusMinus(arr,n);

        bufferedReader.close();
    }
}
```

plusMinus 메소드만 작성하는 문제였는데,
main함수에서 낯선 클래스와 객체를 발견했다.

> BufferedReader

Scanner는 많이 써봤지만 BufferedReader는 써보지 못했다.
BufferedReader는 stream이 다 차거나 null이 아니라면 그 값을 계속 갖고있고, 데이터를 많이 입력받을 경우에 Scanner 보다 메모리가 더 효율적이라고 한다.

InputStreamReader을 입력받아 문자열을 출력해준다.


> map(Integer::parseInt)

메서드 참조를 사용한 것이다.
스트림의 각 문자열 요소를 integer 타입으로 변환해준다. s -> Integer.parseInt(s) 와 동일한 표현이다. "::"는 메서드 참조를 뜻한다.

<br>

### [ 정처기 이론 - 기출문제 ] - 복습

<br>
<br>

## 07/17
### [ JAVA 알고리즘() 문제풀기 - HackerRank ]
```
배열을 입력받아 모두 더한 뒤 각 인덱스에 해당하는 숫자를 빼보고 최댓값과 최솟값을 출력해라.

예)
arr = [1,2,3,4,5]
2+3+4+5 = 14
1+3+4+5 = 13
1+2+4+5 = 12
1+2+3+5 = 11
1+2+3+4 = 10

10 14
```
<br>

```
class Result {

    public static void miniMaxSum(List<Integer> arr) {
        long min = Long.MAX_VALUE; 
        long max = Long.MIN_VALUE; 
        long sum = 0;


        for (int num : arr) {
            sum += num;
        }


        for (int num : arr) {
            long hap = sum - num;
            if (hap < min) {
                min = hap;
            }
            if (hap > max) {
                max = hap;
            }
        }
        System.out.println(min +" "+ max);

    }

}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));

        List<Integer> arr = Stream.of(bufferedReader.readLine().replaceAll("\\s+$", "").split(" "))
            .map(Integer::parseInt)
            .collect(toList());

        Result.miniMaxSum(arr);

        bufferedReader.close();
    }
}
```

<br>

### [ 정처기 이론 - 기출문제 ] - 복습

<br>
<br>

## 07/18
### [ 정처기 이론 ]
- 소프트웨어 구축
    - 프로젝트 계획
    - 요구사항 분석
    - 소프트웨어 설계
    - 소프트웨어 구현

<br>
<br>

## 07/19
### [ 정처기 이론 ]
- 소프트웨어 구축
    - 소프트웨어 테스트
    - 소프트웨어 유지보수

- 데이터베이스
    - 데이터베이스

<br>
<br>

## 07/20
### [ 정처기 이론 ]
- 운영체제
    - 운영체제 종류
    - 페이지 분할 기법
    - 프로세스, 스레드
    - 스케쥴링

<br>
<br>

## 07/21
### [ 정처기 이론 ]
- 운영체제
    - 교착상태

- 네트워크
    - 정보 전송 방식
    - 동기/비동기 전송
    - 프로토콜
    - OSI 7계층
    - HDLC

<br>
<br>

## 07/22
### [ 정처기 이론 ]
- 네트워크
    - 패킷 교환 방식
    - 라우팅
    - vpn 관련 프로토콜
    - IP 주소체계

- 정보보안
    - 양방향 암호화 방식
    - 양방향 암호화 종류
    - 단방향 암호화 방식
    - 서비스 공격 유형
    - 정보보안 솔루션

<br>
<br>

## 07/23
### [ 정처기 이론 - 기출문제 ]
-  웹서비스 종류
- 접근 통제 모델
- 접근 제어 방식
- IP 클래스
- 스키마
- 블록암호 알고리즘
- 테스트 케이스
- 스트링 암호 알고리즘
- 테스트의 목적
- 파일의 구조
