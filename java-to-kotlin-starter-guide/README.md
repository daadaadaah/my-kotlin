# 자바 개발자를 위한 코틀린 입문 강의 Java 코드

- [자바 개발자를 위한 코틀린 입문 강의](https://inf.run/A9p7) Java 코드 입니다!
- 자바 코드를 똑같이 타이핑 하는 시간 역시 아껴드릴 수 있도록 준비해보았습니다.
- 감사합니다!!! :)


## Lec 01. 코틀린에서 변수를 다루는 방법
### 1. 변수 선언 키워드 - var와 val의 차이점
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Lec01Main {

  public static void main(String[] args) {
    long number1 = 10L; // 가변
    final long number2 = 10L; // 불변
  }
}
```
</td>
<td>

```kotlin
fun main() {
  var number1 = 10L // 가변 
  val number2 = 10L // 불변
}
```
</td>
</tr>

<tr>
    <td>
        1. 자바에서는 변수를 `불변`으로 지정해 주고 싶으면, 타입 앞에 `final` 를 붙여주면 된다. <br>
        2. 자바에서는 모든 변수에 타입을 명시적으로 지정해주어야 한다. <br>
    </td>
    <td>
        1. 코틀린에서는 모든 변수에 수정 가능 여부(var/val)를 명시해주어야 한다. 변경 가능하면 var를, 변경 불가능하면 val를 붙여준다. <br>
        2. 코틀린에서는 타입을 명시적으로 작성하지 않아도 된다. 타입을 컴파일러가 자동으로 추론해주기 때문이다. 단, 원하면, 타입을 명시적으로 작성해줄 수도 있다. <br>
        3. 초기값을 지정해주지 않으면, 컴파일 에러가 발생하므로, 타입을 명시해줘야 한다. 또한, 아직 초기화하지 않은 변수를 사용할 경우 컴파일 에러 발생한다.

```kotlin
fun main() {
  // 초기값을 지정해주지 않은 경우 : var
  var number10 // 컴파일 에러 발생, 컴파일러가 타입을 추론할 수 없음

  var number12 = 10L // 타입 추론 가능

  var number11: Long // 명시적으로 타입 지정
  println(number11) // 아직 초기화하지 않은 변수를 사용할 경우 컴파일 에러 발생, Variable 'number11' must be initialized

  number11 = 5
  println(number11) // 값을 지정해주면, 정상 동작함.

  // 초기값을 지정해주지 않은 경우 : val
  val number20 // 컴파일 에러 발생, 컴파일러가 타입을 추론할 수 없음

  val number21 = 10L // 타입 추론 가능

  val number22: Long // 명시적으로 타입 지정
  println(number22) // 아직 초기화하지 않은 변수를 사용할 경우 컴파일 에러 발생, Variable 'number22' must be initialized

  number22 = 5 // 불변이지만, 초기화되지 않는 변수에 한해서 값을 넣어 줄 수 있음
  println(number22) // 값을 지정해주면, 정상 동작함.
}
```
</td>
</tr>
</table>

#### val 컬렉션에는 element를 추가할 수 있다.

<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Lec01Main {

  public static void main(String[] args) {
    final List<Long> list = new ArrayList<>();

    list = new ArrayList<>(); // 컴파일 오류, 컽렉션 자체는 변경 불가

    list.add(10L); // 값 추가는 가능
  }
}
```

</td>
<td>

```kotlin
fun main() {
  val list = ArrayList<Long>()

  list = ArrayList<Long>() // 컴파일 오류, val 컽렉션 자체는 변경 불가

  list.add(10L) // 값 추가는 가능
}
```
</td>
</tr>

<tr>
    <td>
        - 자바에서는 final로 선언된 컬렉션 변수 자체는 변경 불가능하지만, 값 자체는 가능하다. <br>
    </td>
    <td>
        - 코틀린에서도 val로 선언된 컬렉션 변수 자체는 변경 불가능하지만, 값 자체는 가능하다. <br>
</td>
</tr>
</table>

> 코틀린에서 모든 변수는 우선 `val`로 만들고, 꼭 필요한 경우 `var`로 변경하자.


### 2. Kotlin 에서의 Primitive Type
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Lec01Main {

  public static void main(String[] args) {
    long number1 = 10L; // primitive type
    Long number2 = 1_000L; // reference type
  }
}
```

</td>
<td>

```kotlin
fun main() {
  var number1: Long = 10L
  var number2: Long = 1_000L
}
```
</td>
</tr>

<tr>
    <td>
        1. 자바에서는 Primitive Type 과 Reference Type 구분되어 있다. <br>
    </td>
    <td>
        1. 코틀린에서는 Primitive Type 과 Reference Type 구분되어 있지 않다. <br />

- 이펙티브 자바(p.358) 따르면, boxing과 unboxing이 일어나면서 불필요한 객체가 생성되므로, reference 타입을 사용하지 말라고 이야기가 나온다.
- 그럼, 코틀린에서는 모두 Long인데, 성능상 문제는 없는 것인가? 라는 생각이 들 수 있다.
- 코틀린 공식 문서에서는 `숫자, 문자, 불리언과 같은 몇몇 타입은 내부적으로 특별한 표현을 갖는다. 이 타입들은 실행시에 Primitive Value로 표현되지만, 코드에서는 평범한 클래스처럼 보인다.`라고 나와 있다.
- 즉, 프로그래머가 reference type에 대해 boxing/unboxing을 고려하지 않아도 되도록 코틀린이 알아서 처리 해준다.
- 예를 들면, Long 타입 하나로 합쳐져 있지만, 만약 연산을 하게 될 경우, 코틀린이 알아서 똑똑하게 상황에 따라서는 내부적으로 Primitive Type으로 바꿔서 적절히 처리를 해준다는 의미이다.
- 실제 코틀린 코드를 자바로 확인해보자.
  > intellij -> Tools -> Kotlin -> Show Kotlin Bytecode -> Decompile -> 자바 코드 확인
    ```java
    public final class Lec01 {
       public final void main() {
          long number1 = 10L; // Primitive Type 인 long 을 사용하는 것을 알 수 있다.
          long number2 = 1_000L;
       }
    }
    ```
</td>
</tr>
</table>

### 3. Kotlin 에서의 nullable 변수
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Lec01Main {
  public static void main(String[] args) {
    long number1 = 10L;

    number1 = null; // null 불가

    Long number2 = null; // nullable
  }
}
```

</td>
<td>

```kotlin
fun main() {
    var number1: Long = null // null 불가 
    var number2: Long? = null // nullable
}
```
</td>
</tr>

<tr>
    <td>
        1. 자바에서는 Primitive Type 에는 null 값을 가질 수 없고, Reference Type 에서만 가능하다. <br>
    </td>
    <td>
        1. 코틀린에서는 기본적으로 null이 들어 갈 수 없게끔 설계해두었다. 그래서, 그냥 null을 넣으면 컴파일 에러가 난다. 따라서, nullable 한 변수를 만들려면, 타입 뒤에 `?`를 붙여주어야 한다. 이때, 아예 다른 타입으로 간주된다.
</td>
</tr>
</table>


### 4. Kotlin 에서의 객체 인스턴스화
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Lec01Main {
  public static void main(String[] args) {
      Person person = new Person("한영규");
  }
}
```

</td>
<td>

```kotlin
fun main() {
    var person:Person = Person("한영규")
}
```
</td>
</tr>

<tr>
    <td>
        1. 자바에서는 객체를 인스턴스화 할 때 `new`를 붙어야 한다.
    </td>
    <td>
        1. 코틀린에서는 객체를 인스턴스화 할 때 `new`를 붙이지 않아야 한다.
</td>
</tr>
</table>





# Reference
- https://gksdudrb922.tistory.com/261
- 