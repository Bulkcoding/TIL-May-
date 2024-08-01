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
```java
@Entity
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)
@DiscriminatorColumn(name = "dtype") // 싱글테이블에서 구분할 수 있는 타입을 명시
@Getter @Setter
public abstract class Item { // 구현체를 가지고 있어서 추상클래스로 만듦..!

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