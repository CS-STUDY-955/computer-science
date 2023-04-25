# String
## Java의 String
- 문자의 연속적인 집합
- 불변성을 가짐
- 원시 타입이 아닌 객체 타입

## 다음 코드의 출력 결과는?
```java
String s1 = "string";
String s2 = new String("string");
String s3 = String.valueOf("string");

System.out.println(s1.equals(s2));
System.out.println(s1 == s2);
System.out.println(s1 == "string");
System.out.println(s1 == s3);
```
<details>
    <summary>정답</summary>
    <b>true</b> <br>
    <b>false</b> <br>
    <b>true</b> <br>
    <b>true</b> <br>
</details>

## Constant Pool
- 런타임에 생성되는 상수 저장소
- JVM의 Method Area에 존재
- 리터럴 객체, 정수 리터럴, 메서드, 필드, 클래스 정보 등이 저장됨

## String Pool
- 컴파일 타임에 생성되고 값이 저장되는 문자열 상수 저장소
- JVM의 Heap Area에 존재 (GC의 대상)
- 리터럴 객체인 String은 특이하게 Constant Pool에 저장되지 않고 이 영역에 저장됨
- String.intern() 메서드를 사용하면 문자열이 존재하지 않을시 StringPool에 등록하고, 존재하면 StringPool에서 가져옴.

```java
String helloWorld = "HelloWorld";
String world = "World";

System.out.println(helloWorld == new String("HelloWorld"));
System.out.println(helloWorld == "HelloWorld");
System.out.println(helloWorld == ("Hello"+"World"));
System.out.println(helloWorld == ("Hello"+world));
System.out.println(helloWorld == ("Hello"+world).intern());
```
<details>
    <summary>정답</summary>
    <b>false</b> <br>
    <b>true</b> <br>
    <b>true</b> <br>
    <b>false</b> <br>
    <b>true</b> <br>
</details>


## 참고
- [String 객체와 문자열 상수](https://www.codelatte.io/courses/java_programming_basic/PP95VV3NZJM71V14)
- [Constant Pool과 String Pool](https://blog.breakingthat.com/2018/12/21/java-constant-pool%EA%B3%BC-string-pool/)
- [intern() 심화](https://www.latera.kr/blog/2019-02-09-java-string-intern/)
