## 08/01
### [ spring boot & jpa 강의 수강 3일차 ]
#### **section2 - 3 ( 엔티티 클래스 개발 )**
![Alt text](<화면 캡처 2024-08-03 132254.png>)
Album, Book, Movie는 Item 클래스의 자식클래스이다.

이 관계에서 Item 클래스에는 @Inheritance라는 어노테이션을 지정해줘야하는데,

strategy = InheritanceType에는 3가지 종류의 전략이 있다.

<br>

> @Inheritance(strategy = InheritanceType.JOINED)

가장 정규화된 스타일로 하는 것.

부모 클래스의 테이블이 공통속성을 가지고 자식 테이블들은 각자의 고유한 컬럼들을 따로 갖는다.

<br>

> @Inheritance(strategy = InheritanceType.SINGLE_TABLE)

한 테이블에 모든 자식의 정보를 다 때려박는 것. 디폴트로 설정됨.

<br>

> @Inheritance(strategy = InheritanceType.TABLE_PER_CLASS)

부모 클래스에 대한 테이블은 존재하지 않는다.
각 자식 클래스 별로 자신만의 테이블을 갖는데,
이때 부모가 갖고 있어야 할 고유한 속성들을 모든 자식 클래스가 자신의 테이블에 갖고 있는 방식

여기서는 @Inheritance(strategy = InheritanceType.SINGLE_TABLE) 방식을 채택했다.

<추상클래스(부모)>

 싱글테이블에서 구분할 수 있는 타입을 명시하는 것이 dtype이다.

```java
@Entity
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)
@DiscriminatorColumn(name = "dtype")
@Getter @Setter
public abstract class Item {

    @Id
    @GeneratedValue
    @Column(name="item_id")
    private Long id;

    // 상속관계 매핑
     private String name;
     private int price;
     private int stockQuantitty;

    @ManyToMany(mappedBy = "items")
    private List<Category> categories = new ArrayList<>();

}
```
<br>

<자식클래스(Albums)>

싱글테이블 전략을 채택했기 때문에 저장할때 구분할 수 있는 것이 있어야 한다.
그러기 위해서 @DiscriminatorValue("A") 어노테이션을 붙이고 구분할 값을 넣어주면 된다.

```java
@Entity
@DiscriminatorValue("A")
@Getter
@Setter
public class Album extends Item {
}
```
<br>

<자식클래스(Book)>

```java
@Entity
@DiscriminatorValue("B")
@Getter
@Setter
public class Book extends Item {

    private String author;
    private String isbn;
}
```

<br>

<자식클래스(Movie)>
```java
@Entity
@DiscriminatorValue("M")
@Getter
@Setter
public class Movie extends Item {

    private String director;
    private String actor;
}
```

<br>
<br>

> Enum

Enum클래스를 필드로 가지고 올때 @Enumerated을 지정해줘야하는데, 타입이 두 가지가 있다.

- @Enumerated(EnumType.ORDINAL)
    - default 타입. 절대로쓰면 안된다.
    - 처음에 man, woman을 enum값으로 넣으면 1,2 순서대로 값을 갖는데, 중간에 man, human, woman 처럼 값이 들어와 버리면 순서대로 1,2,3을 갖게 되므로 값이 꼬여버린다. 그래서 절대로 쓰면 안된다.

- @Enumerated(EnumType.STRING)
    - String은 말 그대로 문자값을 그대로 넣기 때문에 안정적이다.


```java
@Entity
@Getter
@Setter
public class Delivery {

    @Id
    @GeneratedValue
    @Column(name = "delivery_id")
    private Long id;

    @OneToOne(mappedBy = "delivery", fetch = LAZY)
    private Order order;

    @Embedded
    private Address address;

    @Enumerated(EnumType.STRING)
    private DeliveryStatus status;  // READY, COMP
}
```

```java
public enum DeliveryStatus {
    READY, COMP
}
```

<br>
<br>

## 08/02
### [ spring boot & jpa 강의 수강 4일차 ]
#### **section2 - 5 ( 엔티티 설계시 주의점)**

- 엔티티를 변경할 때는 Setter 대신에 변경 지점이 명확하도록 변경을 위한 비즈니스 메서드를 별도로 제공해야 한다. (Setter 남발하지 않기)
    - 변경포인트가 많아서 에러가 나서 유지보수시, 특정엔티티가 어디서 어떻게 변경됐는지 알 수가 없기 때문.
- 모든 연관관계는 지연로딩으로 설정
    - 즉시로딩(EAGER)은 연관된 테이블들을 전부 다 끌어모으기 때문에 어떤 SQL이 실행될지 추적하기 어렵고, 특히 N+1 문제가 자주 발생한다.
    - 실무에서 모든 연관관계는 지연로딩(LAZY)로 설정해야하 한다.
    - @XToOne(OneToOne, ManyToOne) 관계는 기본이 즉시로딩이므로 직접 지연로딩으로 설정해야 한다
    - XTOMany는 기본이 지연로딩이기 때문에 그대로 두어도 된다.
- 컬렉션은 필드에서 초기화하자.
```java
Member member = new Member();
System.out.println(member.getOrders().getClass());
em.persist(member);         // db에 영속화 하겠다는 뜻
System.out.println(member.getOrders().getClass());
```
이런 코드가 있다고 가정하자.

출력결과는 다음과 같다.
```
class java.util.ArrayList
class org.hibernate.collection.internal.PersistentBag
```
같은 코드인데, 출력값이 달라졌다. 그 이유는

영속화 되면 하이버네이트가 컬렉션을 감싸기 때문에 결과가 달라지게된다. 이제 이 컬렉션을 바꾸게 되면 하이버네이트가 원하는대로 동작을 안하게 되는 문제가 발생한다.
따라서 컬렉션은 필드에서 바로 초기화 하는 것이 안전하다.
