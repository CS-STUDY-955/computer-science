# Java Stream API 

## 1. 개념
+ Java 8에서 추가
+ Stream은 데이터의 흐름
+ 배열, 컬렉션 인스턴스를 가공해 원하는 결과를 얻을 수 있음
+ 람다를 이용해 코드의 양을 줄일 수 있음

\* InputStream, OutputStream 등 입출력에서 말하는 Stream과는 다른 개념

<br>

***
## 2. 생성
```java
// Array Stream
int[] arr = {1, 2, 3};
IntStream arrayStream = Arrays.stream(arr);

IntStream intStream = IntStream.of(1, 2, 3, 4);

// Collection Stream
ArrayList<Integer> list = new ArrayList<Integer>(Arrays.asList(1, 2, 3));
Stream<Integer> listStream = list.stream();

// 람다식으로 초기화
Stream<Integer> iteratedStream = 
            Stream.iterate(30, n -> n + 2).limit(5); 
iteratedStream.forEach((s) -> System.out.println(s));
// [30, 32, 34, 36, 38]
```
<br>

***
## 3. 가공하기
### 3.1 Filtering
+ 스트림 내 요소들을 하나씩 평가해 걸러내는 작업
+ boolean을 리턴하는 함수형 인터페이스를 이용해야함
```java
IntStream example2Stream = IntStream.rangeClosed(1, 10);
example2Stream.filter(i -> i % 2 == 0).forEach(System.out::println);
// 2 4 6 8 10
```

### 3.2 Mapping
+ 스트림 내 요소들을 하나씩 특정 값으로 변환해줌
+ 람다를 인자로 받음
```java
Stream<Integer> stream = 
  productList.stream()
  .map(Product::getAmount);
// [23, 14, 13, 23, 13]
```

### 3.3 Sorting
```java
IntStream.of(14, 11, 20, 39, 23)
  .sorted()
  .boxed()
  .collect(Collectors.toList());
// [11, 14, 20, 23, 39]
```
##
<br>

***
참고 <br> 
[Java 스트림 Stream (1) 총정리](https://futurecreator.github.io/2018/08/26/java-8-streams/) <br>
[Java 스트림 Stream (2) 고급](https://futurecreator.github.io/2018/08/26/java-8-streams-advanced/) <br>
[자바의 정석 - 스트림(Stream)](https://ryan-han.com/post/dev/java-stream/)
