# 직렬화(Serialization)

- 자바 시스템 내부에서 사용되는 객체 또는 데이터를 외부의 자바 시스템에서도 사용할 수 있도록 바이트(byte)형태로 데이터를 변환하는 기술
- 큰 의미에서 바이트로 변환된 데이터를 다시 객체로 변환하는 기술인 역직렬화(Deserialization)를 포함하여 의미함

<br>

## 자바 직렬화 조건

- 기본 타입(Primitive), java.io.Serializable 인터페이스를 상속받은 객체

```java
import java.io.*;

public class Person implements Serializable {
    private static final long serialVersionUID = 1L;
    private String name;
    private int age;

    ...
}
```

<br>

## 자바 직렬화 방법

- java.io.ObjectOutputStream 객체를 이용

```java
import java.io.*;

public class Person implements Serializable {
    private static final long serialVersionUID = 1L;
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
	public String toString() {
		return "Person [name=" + name + ", age=" + age + "]";
	}

	public static void main(String[] args) {
        Person person = new Person("John", 30);

        try {
            FileOutputStream fileOut = new FileOutputStream("person.ser");
            ObjectOutputStream out = new ObjectOutputStream(fileOut);
            out.writeObject(person);
            out.close();
            fileOut.close();
            System.out.println("Serialized data is saved in person.ser");
        } catch (IOException i) {
            i.printStackTrace();
        }
    }
}
```

<br>

## 역직렬화 조건

- 직렬화된 객체의 클래스가 클래스 패스에 존재하고 import 되어 있어야 한다.
- 이때 직렬화와 역직렬화를 진행하는 시스템이 서로 다를 수 있음을 고려해야함
- 직렬화 대상 객체는 동일한 serialVersionUID를 가지고 있어야함

<br>

## 역직렬화 방법

- java.io.ObjectInputStream을 이용

```java
    try {
        FileInputStream fileIn = new FileInputStream("person.ser");
        ObjectInputStream in = new ObjectInputStream(fileIn);
        Person restoredPerson = (Person) in.readObject();
        in.close();
        fileIn.close();
        System.out.println("Deserialized data:");
        System.out.println(restoredPerson);
    } catch (IOException i) {
        i.printStackTrace();
    } catch (ClassNotFoundException c) {
        System.out.println("Person class not found");
        c.printStackTrace();
    }
```

<br>

## serialVersionUID (SUID)

- 역직렬화시 클래스 구조가 변경 되는 경우

클래스 구조 변경 전 출력 결과

```
Deserialized data:
Person [name=John, age=30]
```

클래스 구조 변경 후

```java
public class Member implements Serializable {
    private String name;
    private int age;
    private String email;
}
```

```
java.io.InvalidClassException: test.Person; local class incompatible: stream classdesc serialVersionUID = -3637310856900372143, local class serialVersionUID = -2921636307248833683
```

seriailVersionUID의 정보가 일치하지 않아 예외 발생

- SUID가 필수 값은 아니며, 선언되어 있지 않으면 클래스의 기본 해쉬값을 사용함
- 호환 가능한 클래스는 직렬화 클래스와 역직렬화 클래스의 SUID 값이 같아야함

클래스에 default SUID를 명시한 경우

```java
public class Person implements Serializable {
	private static final long serialVersionUID = 1L;
    private String name;
    private int age;
    private String email;
}
```

```
Deserialized data:
Person [name=John, age=30, email=null]
```

- 클래스 구조가 변경되어도 직렬화/역직렬화를 할 수 있음
- 단, 이때 변수 타입이 다르면 예외 발생
- 변수를 제거하거나 변수명을 바꾸면 데이터가 누락됨

```
Deserialized data:
Person [name1=null, age1=0]
```

- SUID는 개발 시 직접 관리해야함

<br>
<hr>

- 자바 직렬화 외에도 특정 라이브러리를 이용하여 데이터를 csv, JSON의 문자열 형태로 변환하거나 프로토콜 버퍼, Apache Avro 등으로 직렬화하여 추출하는 것이 가능

## 자바 직렬화의 사용 이유

- JVM 메모리에 상주되어있는 객체 데이터를 영속화 -> 시스템이 종료되어도 데이터 보존
- 객체 상태 유지 용이 -> 직렬화/역직렬화가 간단하고, 데이터 타입이 자동으로 맞춰져 사용하기 쉬움
- 플랫폼 간 호환 가능 -> 자바 직렬화는 자바의 표준 기능으로 모든 플랫폼에서 사용 가능

<br>

[자바 직렬화, 그것이 알고싶다. 훑어보기편 | 우아한형제들 기술블로그](https://techblog.woowahan.com/2550/)<br>
[자바 직렬화, 그것이 알고싶다. 실무편 | 우아한형제들 기술블로그](https://techblog.woowahan.com/2551/)<br>
