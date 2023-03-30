# Reflection
## 정적 언어 VS 동적 언어

|     | 정적 타입 언어                   | 동적 타입 언어                            |
|-----|----------------------------|-------------------------------------|
| 정의  | 컴파일 시점에 자료형이 정해지는 언어       | 런타임 시점에 자료형이 정해지는 언어                |
| 특징  | 타입 에러를 초기에 잡을 수 있어 안정성이 높음 | 런타임까지 타입에 대한 결정 미룰 수 있기 때문에 유연성이 높음 |
| 언어  | Java, C, C++, ...          | Groovy, Python, JavaScript, ...     |

## Reflection 이란?
- 구체적인 클래스 타입을 알지 못해도 클래스의 정보에 접근할 수 있도록 해주는 자바 API
- 정적 타입 언어를 동적 타입 언어처럼 사용하게 해주는 기술
- JVM에 의해 각종 클래스 정보가 Method Area에 저장되고, 이 영역을 확인하여 정보를 가져옴

## Example
```java
public class Car {
    private final String name;
    private int position;

    public Car(String name, int position) {
        this.name = name;
        this.position = position;
    }

    public void move() {
        this.position++;
    }

    public int getPosition() {
        return position;
    }
}
```
```java
public static void main(String[] args) {
    Object obj = new Car("foo", 0);
    obj.move();    // 컴파일 에러 발생 java: cannot find symbol
}
```
```java
public static void main(String[] args) throws Exception {
    Object obj = new Car("foo", 0);
    Class carClass = Car.class;
    Method move = carClass.getMethod("move");

    // move 메서드 실행, invoke(메서드를 실행시킬 객체, 해당 메서드에 넘길 인자)
    move.invoke(obj, null);

    Method getPosition = carClass.getMethod("getPosition");
    int position = (int)getPosition.invoke(obj, null);
    System.out.println(position);
    // 출력 결과: 1
}
```

## 1. IDE Auto Completion
![auto completion](https://user-images.githubusercontent.com/50614241/228832281-1f1ee7ab-a19d-4efd-9222-e623a56102f7.png)

## 2. Class.forName()
![forName](https://user-images.githubusercontent.com/50614241/228832287-f98d1275-fe42-4d7e-9fd1-163ff5268926.png)

## 3. Annotation
```java
@Target({ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
public @interface MyAnnotation {
        String value() default "MyAnnotation : default value";
}
```
```java
class MyObject {
    @MyAnnotation
    public void testMethod1() {
        System.out.println("This is testMethod1");
  }

    @MyAnnotation(value = "My new Annotation")
    public void testMethod2() {
        System.out.println("This is testMethod2");
  }
}
```
```java
public class MyMain {
    public static void main(String[] args) {
        Method[] methodList = MyObject.class.getMethods();

        for (Method method : methodList) {
            if(method.isAnnotationPresent(MyAnnotation.class)) {
                MyAnnotation annotation=method.getDeclaredAnnotation(MyAnnotation.class);
                String value=annotation.value();
                System.out.println(method.getName() + ":" + value);
            }
        }
    }
}
```
![result](https://user-images.githubusercontent.com/50614241/228832933-b02312bb-e6f1-48ad-ae08-c51e24fb2fc2.png)

## 단점
1. 코드가 지저분해진다. -> 유지보수성 저하
2. 추상화가 깨진다. -> 보안 이슈 발생
3. 컴파일 타임에 최적화를 할 수 없어 성능 오버헤드가 발생한다.