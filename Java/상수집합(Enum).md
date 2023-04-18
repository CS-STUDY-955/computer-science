# 상수집합 (Enum)
- Enum은 서로 관련있는 여러 개의 상수 집합을 정의할 때 사용하는 자료형
- 상수란 값이 변하지 않는 고정 값을 의미

## 만들기
```java
public class Main{
    enum Menu{
        ESPRESSO,
        AMERICANO,
        CAFE_LATTE,
        CAFE_MOCA
    };

    public static void main(String[] args) {
        System.out.println(Menu.ESPRESSO);  // ESPRESSO 출력
        System.out.println(Menu.AMERICANO);  // AMERICANO 출력
        System.out.println(Menu.CAFE_LATTE);  // CAFE_LATTE 출력
        System.out.println(Menu.CAFE_MOCA);  // CAFE_MOCA 출력
    }
}
```

## 사용
```java
for(Menu menu: Menu.values()) {
    System.out.println(menu);  // 순서대로 ESPRESSO, AMERICANO, CAFE_LATTE, CAFE_MOCA 출력
}
// .values() 메서드는 enum의 배열 리턴
```

## Final과의 차이
```java
public static final int MONDAY = 1;
public static final int TUESDAY = 2;
public static final int WEDNESDAY = 3;
public static final int THURSDAY = 4;
public static final int FRIDAY = 5;
public static final int SATURDAY = 6;
public static final int SUNDAY = 7;
```
- 문제점
    1. 가독성 저하. 상수의 이름만으로는 의미 파악하기 힘듦
    2. 오타 등의 실수 발생 가능 ex. TUESDAY, THUESDAY
    3. 상수들이 관련있는 것들끼리 그루핑되어 있지 않음

```JAVA
public enum DayOfWeek {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}
```
- 장점
    1. 상수의 다양한 기능 사용 가능
        - switch
        - method
        - 상수 비교(==) 가능
        - values() 사용하면 배열 형태로 반환
        - name() 사용하면 상수의 이름을 문자열로 반환
        - 기타 다양한 기능 제공
    2. 가독성 향상
    3. 오타 등 실수 발생 가능성 저하 (올바른 이름을 지정하려면 그대로 사용해야하기 때문)
    4. 관련있는 상수들끼리 그루핑할 수 있음


## 단점
1. 유지보수 어려워질 수 있음
    - enum은 내부에 모든 상수들이 정의되므로, 상수가 많아지면 해당 크기가 커져서 가독성이 저하될 수 있음
2. 불필요한 메모리 사용 가능성
    - enum의 경우 모든 상수가 메모리에 미리 할당되어, 상수가 많은 경우 메모리 사용량 증가
3. 코드가 상대적으로 복잡해질 수 있음
    - enum은 다양한 기능 제공하여, 불필요하게 구현하면 코드 복잡도 향상
    - 필요한 기능만 구현해야 함

## 참고
- https://wikidocs.net/157271
