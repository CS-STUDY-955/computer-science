# String
## String
- 문자열
- 문자의 연속적인 집합
- 원시 타입이 아닌 객체 타입

## 다음 코드의 출력 결과는?
```java
final String s1 = "string";
final String s2 = new String("string");
final String s3 = String.valueOf("string");

System.out.println(string.equals(string2));
System.out.println(s1 == string2);
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
- 런타임에 생성되는 static 상수 저장소
- JVM의 Heap 영역(Method Area)에 존재
- 
```java
String s1 = "Hello";
String s2 = "World";
String s3 = s1 + s2;
String s4 = "Hello World";

System.out.println((s1 + s2) == s3);
System.out.println(s3 == s4);
System.out.println((s1 + s2) == s4);
System.out.println((s1 + s2).intern() == s3);
System.out.println((s1 + s2).intern() == s4);
System.out.println(s3.intern() == s4);
```

## 참고
- https://blog.naver.com/adamdoha/222817943149
- https://www.latera.kr/blog/2019-02-09-java-string-intern/

## 퀴즈 정답
