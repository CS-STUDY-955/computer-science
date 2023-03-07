# ArrayList vs LinkedList
## ArrayList
- 실제 배열과 비슷하게 저장되고 작동하는 List
- 바로 원하는 인덱스로 접근할 수 있는 Random Access 방식
- 조회 연산에 유리

![arraylist](https://user-images.githubusercontent.com/50614241/223421820-e4bf02dc-95c3-46b2-b401-462815dad6a0.png)

## LinkedList
- 포인터를 이용해 다음 원소에 접근하는 방식으로 작동하는 List
- 원하는 인덱스까지 순차적으로 접근해야하는 Sequential Access 방식
- 삽입, 삭제 연산에 유리

![linkedlist](https://user-images.githubusercontent.com/50614241/223421819-7850ae8c-b39e-41b4-919a-6ae16bc838af.png)

## 시간복잡도 비교
|                  | ArrayList | LinkedList |
|------------------|-----------|------------|
| get(index)       | O(1)      | O(N)       |
| add(item)        | O(N)      | O(1)       |
| add(index, item) | O(N)      | O(N)       |

## 실사용시 차이점
```java
/**
 * 굉장히 많이 호출되는 메서드
 * 리스트 내의 모든 원소를 출력한다.
 * ArrayList가 유리할까? LinkedList가 유리할까?
 */
public void print(List<Object> list) {
    for(int i=0; i<list.size(); i++) {
        System.out.print(list.get(i) + " ");
    }
}
```

```java
/**
 * list로 LinkedList가 올 경우, get() 메서드가 이미 O(n)의 시간복잡도를 지니기 때문에
 * 실질적으로 위의 코드는 O(n^2)의 시간복잡도를 가지게 된다.
 * 따라서 아래의 코드를 사용하는 것이 권장된다.
 */
public void print(List<Object> list) {
    for(int elem: list) {
        System.out.print(elem + " ");
    }
}
```

## 번외)LinkedList vs ArrayDeque
- 그런데 우리는 큐 인테페이스의 구현체를 생성할 때 보통 LinkedList를 사용하지 않는다. 이유가 무엇일까??
- 다들 알고있듯이 보편적으로 ArrayDeque를 사용하며, 자바 공식 문서에서도 Stack과 Queue는 Deque로 구현하는 것이 완전하고 일관된 구현이라고 설명하고 있다.
- LinkedList는 사실상 Tree 등 다른 자료구조의 근간으로 이해하고 있으면 되는 수준이다.

### ArrayDeque 사용 이유
  1. Stack은 구현 클래스인 Vector를 상속받기도 하며, 레거시 클래스라 기본적으로 성능이 좋지 않다.
  2. Deque는 Thread를 고려하지 않도록 설계되어 대부분의 경우 성능이 좋다.
  3. ArrayDeque는 포인터를 사용하지 않으므로 메모리 효율적이다.
  4. ~~컴파일시 코드 캐싱이 효율적으로 이루어진다.~~