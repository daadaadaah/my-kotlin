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

## Lec 02. 코틀린에서 null을 다루는 방법
### 1. Kotlin 에서의 null 체크
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Lec01Main {
    // A로 시작하는 문자인지 판단하는 함수
    // 안전하지 않은 코드, 
    // 왜냐하면 str에 null이 들어올 수 있는데, 이때 NPE가 발생하기 때문에
    public boolean startsWithA(String str) {
        return str.startsWith("A");
    }

    // 위 코드를 null 에 대해 안전한 함수로 바꾸는 방법 3가지
    // 방법 1 : str이 null일 경우 Exception을 낸다
    public boolean startsWithA1(String str) {
        if (str == null) {
            throw new IllegalArgumentException("null이 들어왔습니다");
        }
        return str.startsWith("A");
    }

    // 방법 2 : str이 null일 경우 null을 반환한다
    public Boolean startsWithA2(String str) {
        if (str == null) {
            return null;
        }
        return str.startsWith("A");
    }

    // 방법 3 : str이 null일 경우 false를 반환한다
    public boolean startsWithA3(String str) {
        if (str == null) {
            return false;
        }
        return str.startsWith("A");
    }
}
```

</td>
<td>

```kotlin

fun main() {
    val isStartedWithA0 = startsWithA0(null) // 컴파일 에러가 난다. 왜냐하면, str는 nullable 한 변수가 아니므로,
    println("A로 시작하는 문자인가요? : $isStartedWithA0")

    val isStartedWithA1 = startsWithA1(null)
    println("A로 시작하는 문자인가요? : $isStartedWithA1")
    
    
    
    
}

fun startsWithA0(str: String): Boolean { // null 불가 boolean 리턴
    return str.startsWith("A")
}

// str이 null일 경우 Exception을 낸다
fun startsWithA1(str: String?): Boolean { // null 불가 boolean 리턴
    if (str == null) {
        throw IllegalArgumentException("null이 들어왔습니다")
    }
    return str.startsWith("A")
}

// str이 null일 경우 null을 반환한다
fun startsWithA2(str: String?): Boolean? { // nullable Boolean 리턴
    if (str == null) {
        return null
    }
    return str.startsWith("A")
}

// str이 null일 경우 false를 반환한다
fun startsWithA3(str: String?): Boolean { // null 불가 boolean 리턴
    if (str == null) {
        return false
    }
    return str.startsWith("A")
}
```
</td>
</tr>

<tr>
    <td>
        1. 자바에서는 객체를 인스턴스화 할 때 `new`를 붙어야 한다.
    </td>
    <td>
        - 코틀린에서는 null이 가능한 타입을 완전히 다르게 취급한다.
        - null이 가능한 타입만을 위한 기능은 없나? 있다.
            1) Safe call : null이 아니면 실행하고, null이면 실행하지 않는다.

</td>
</tr>
</table>




### 2. Safe Call과 Elvis 연산자
```kotlin
fun main() {
    // Safe Call : "?."을 사용한 Safe Call: str이 null이 아니면 실행하고 null이면 실행하지 않고 그대로 null을 반환한다.
    var str1: String? = "ABC"
    
    println(str1.length) // 컴파일 오류

    println(str1?.length)

    var str2: String? = null

    println(str2.length) // 컴파일 오류

    println(str2?.length) // null

    // Elvis 연산자 :  safe call과 함께 사용하는 연산자로, 앞의 연산 결과가 null 이면 뒤의 값을 사용
    var str3: String? = null

    val str3Length = str3?.length ?: 0
    
    println(str3Length) // 0
}

```

> 왜 Elvis 연산자인가?
>
> - "?:"를 90도 회전하면 엘비스 프레슬리와 닮았다고 해서 그렇다고 한다.

<table>
<tr>
  <td>kotlin(Safe Call과 Elvis 연산 사용하기 전)</td>
  <td>kotlin(Safe Call과 Elvis 연산 사용하기 후)</td>
</tr>

<tr>
<td>

```kotlin
// str이 null일 경우 Exception을 낸다
fun startsWithA1(str: String?): Boolean { // null 불가 boolean 리턴
    if (str == null) {
        throw IllegalArgumentException("null이 들어왔습니다")
    }
    return str.startsWith("A")
}

// str이 null일 경우 null을 반환한다
fun startsWithA2(str: String?): Boolean? { // nullable Boolean 리턴
    if (str == null) {
        return null
    }
    return str.startsWith("A")
}

// str이 null일 경우 false를 반환한다
fun startsWithA3(str: String?): Boolean { // null 불가 boolean 리턴
    if (str == null) {
        return false
    }
    return str.startsWith("A")
}
```

</td>
<td>

```kotlin
fun startsWithA1(str: String?): Boolean {
    return str?.startsWith("A") ?: throw IllegalArgumentException("null이 들어왔습니다")
}

fun startsWithA2(str: String?): Boolean? {
    return str?.startsWith("A")
}

fun startsWithA3(str: String?): Boolean {
    return str?.startsWith("A") ?: false
}
```
</td>
</tr>
</table>

> Elvis 연산자는 early return에도 사용할 수 있다.
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Lec01Main {
    
    public long calculate(Long number) {
        if (number == null) {
            return 0;
        }
        
        return number;
    }
}
```

</td>
<td>

```kotlin
fun calculate(number: Long?): Long {
    return number ?: return 0
}
```
</td>
</tr>

</table>






### 3. null 아님 단언 : !!
- nullable type이지만, 절대 null될 수 없는 경우라면 non-null asserted call("!!.")을 사용할 수 있다.

```kotlin
// str가 null 값을 가질 수 없다고 한다면, 오히려 매개변수의 타입을 String? 이 아닌 String 으로 
// 하는게 더 좋지 않을까? 이렇게 될 경우, 개발자 실수로 null을 입력해줄 경우, 컴파일 에러가 발생하기 때문에, 좀더 나을 것 같은데
fun startsWithA1(str: String?): Boolean {
  return str!!.startsWith("A")
}
```


### 4. 플랫폼 타입
- 플랫폼 타입 : 코틀린이 null 관련 정보를 알 수 없는 타입으로, 런타임시 Exception이 발생할 수 있다.
- 

## Lec 03. 코틀린에서 Type을 다루는 방법
### 1. 기본 타입
1. 코틀린에서는 선언된 기본값을 보고 타입을 추론한다.
```kotlin
val number1 = 3 // Int
val number2 = 3L // Long
val number3 = 3.0f // Float
val number4 = 3.0 // Double
```

2. 기본 타입간의 변환
- 자바에서 기본 타입간의 변환은 `암시적으로` 이루어질 수 있다.
- int 타입의 값이 long 타입으로 암시적으로 변경되었다. Java에서 더 큰 타입으로는 암시적 변경이 이루어질 수 있다.
```java
int number1 = 4;
long number2 = number1; // 더 큰 타입으로 암시적 변경
```

- 코틀린에서 기본 타입간의 변환은 to변환타입()을 사용해서 `명시적으로` 이루어져야 한다.
```kotlin
val number1 = 3 // Int 로 타입 추론됨.
val number2: Long = number1 // 컴파일 오류
val number2: Long = number1.toLong() // 명시적 변환
```

- 변수가 nullable이라면 적절한 처리가 필요하다.
```kotlin
val number1: Int? = 3

val number2: Long = number1.toLong() // 컴파일 에러, number1이 null일 수도 있기 때문에

val number2: Long = number1?.toLong() ?: 0L

```

### 2. 타입 캐스팅
<img width="440" alt="스크린샷 2024-02-10 오후 8 58 14" src="https://github.com/daadaadaah/my-kotlin/assets/60481383/1163b861-6808-47f9-8c4e-292121afbc3d">
<img width="609" alt="스크린샷 2024-02-10 오후 8 59 36" src="https://github.com/daadaadaah/my-kotlin/assets/60481383/9d66f59f-9df1-44db-8ba2-e871a7d6f8d6">
<img width="626" alt="스크린샷 2024-02-10 오후 9 00 16" src="https://github.com/daadaadaah/my-kotlin/assets/60481383/616b48f2-d855-4bef-b511-4bf7f2653bc2">

  
## Lec 04. 코틀린에서 연산자를 다루는 방법
### 1. 단항 연산자 / 산술 연산자
- 자바와 코틀린 완전 동일하다.

### 2. 비교 연산자와 동등성, 동일성
#### 비교 연산자
- 자바와 코틀린 사용법이 동일하다.
- 자바와 다르게, 코틀린에서는 객체를 비교할 때 비교 연산자를 사용하면 자동으로 `compareTo`를 호출해준다.
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Main {
  public static void main(String[] args) {
    JavaMoney money1 = new JavaMoney(1_000L);
    JavaMoney money2 = new JavaMoney(2_000L);
     
    if (money1.compareTo(money2) > 0) {
      System.out.println("Money1이 Money2보다 금액이 큽니다");
    }
  }
}

public class JavaMoney implements Comparable<JavaMoney> {
 
  private final long amount;
 
  public JavaMoney(long amount) {
    this.amount = amount;
  }
 
  public JavaMoney plus(JavaMoney other) {
    return new JavaMoney(this.amount + other.amount);
  }
 
  @Override
  public int compareTo(@NotNull JavaMoney o) {
    return Long.compare(this.amount, o.amount);
  }
 
  @Override
  public boolean equals(Object o) {
    if (this == o) return true;
    if (o == null || getClass() != o.getClass()) return false;
    JavaMoney javaMoney = (JavaMoney) o;
    return amount == javaMoney.amount;
  }
 
  @Override
  public int hashCode() {
    return Objects.hash(amount);
  }
 
  @Override
  public String toString() {
    return "JavaMoney{" +
        "amount=" + amount +
        '}';
  }
 
}
```

</td>
<td>

```kotlin
fun main() {
  val money1 = JavaMoney(2_000L)
  val money2 = JavaMoney(1_000L)
   
  if (money1 > money2) { // 코틀린에서는 비교 연산자 상황이 되면, 자동으로 compareTo를 자동으로 호출해준다.
      println("Money1이 Money2보다 금액이 큽니다")
  } 
}

```
</td>
</tr>
</table>

#### 동일성(Idenntity)과 동등성(Equality)
- 동일성 : 두 객체가 동일한 객체인가? 즉, 주소가 같은가
- 동등성 : 두 객체의 값이 같은가?

<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Main {
  public static void main(String[] args) {
    JavaMoney money1 = new JavaMoney(1_000L);
    JavaMoney money2 = money1;
    JavaMoney money3 = new JavaMoney(1_000L);
    
    System.out.println(money1 == money2); // true, 동일성
    System.out.println(money1 == money3); // false
    System.out.println(money1.equals(money3)); // true, 동등성
  }
}
```

</td>
<td>

```kotlin
fun main() {
  val money1 = JavaMoney(2_000L)
  val money2 = money1
  val money3 = JavaMoney(2_000L)
  
  println(money1 === money2) // ture, 동일성
  println(money1 === money3) // false
  println(money1 == money3) // ture, 동등성 
}

```
</td>
</tr>
<tr>
    <td>
        - 자바에서는 동일성에 ==을 사용하고, 동등성에 equals를 직접 호출 <br/>
    </td>
    <td>
        - 코틀린에서는 동일성에 ===을 사용하고, 동등성에 ==을 호출 -> ==을 사용하면 간접적으로 equals를 호출해준다. <br/>
</td>
</tr>
</table>

### 3. 논리 연산자 / 코틀린에 있는 특이한 연산자
#### 논리 연산자
- 자바와 코틀린이 완전히 동일하다.
- 자바처럼 코틀린에서도 Lazy 연산을 수행한다.

```kotlin
fun main() {
    if (fun1() || fun2()) { // fun1()이 true이므로, fun2()을 호출하지 않고 바로 "본문"을 출력한다. -> lazy 연산
        println("본문")
    }

    // 결과
    // fun1
    // 본문

    if(fun2() && fun1()) { // fun1()이 false이므로, fun1()을 호출하지 않고 바로 "본문"을 출력한다. -> lazy 연산
        println("본문")
    }

    // 결과
    // fun2
    // 본문

}
 
fun fun1(): Boolean {
    println("fun1")
    return true
}
 
fun fun2(): Boolean {
    println("fun2")
    return false
}

```

#### 코틀린에 있는 특이한 연산자
1. in / !in
- 컬렉션이나 범위에 포함되어 있다. 포함되어 있지 않다.
2. a..b
- a부터 b까지의 범위 객체를 생성한다.
3. a[i]
- a에서 특정 index i로 값을 가져온다.
```kotlin
val str = "ABC"
println(str[2]) // C
```
4. a[i] = b
- a에서 특정 index i에 b를 넣는다.


### 4. 연산자 오버로딩
- 코틀린에서는 객체마다 연산자를 직접 정의할 수 있다.
```kotlin
data class Money (
    val amount: Long
) {
    operator fun plus(other: Money): Money {
        return Money(this.amount + other.amount)
    }
}

fun main() {
    val money1 = Money(2_000L)
    val money2 = Money(1_000L)
    println(money1 + money2)
    
    // 결과
    Money(amount=3000)
}
```




<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Main {
  public static void printAgeIfPerson(Object obj) {
    if (obj instanceof Person) {
      Person person = (Person) obj;
      System.out.println(person.getAge());
    }

    if (obj instanceof Person) {
      System.out.println(obj.getAge()); // 에러가 남. Cannot resolve method 'getAge' in 'Object'
    }

    // not 의미 : obj가 Person 타입이 아니라면
    if (!(obj instanceof Person)) {
      Person person = (Person) obj;
      System.out.println(person.getAge());
    }
  }
}
```

</td>
<td>

```kotlin
fun printAgeIfPerson(obj: Any) {
  if (obj is Person) {
    val person = obj as Person
    println(person.age)
  }
  
  // 스마트 캐스트
  // 한 번 코틀린 컴파일러가 컨텍스트를 분석해가지고
  if (obj is Person) {
    println(obj.age)
  }
  
  // not 의미 : obj가 Person 타입이 아니라면
  if (obj !is Person) {
    println(obj.age)
  }

  // 자바처럼 이렇게도 되긴 함.
  if (!(obj is Person)) {
    println(obj.age)
  }
}

```
</td>
</tr>
<tr>
<td>
1. 자바에서는 `instanceof`로 객체의 타입을 판별한다. <br />
2. 자바에서는 `(Person) obj`으로 타입 캐스팅한다. <br />
3. 자바에서는 스마트 캐스트 같은 기능을 지원하지 않는다. <br />
</td>
<td>
1. 코틀린에서는 `is`로 객체의 타입을 판별한다. <br />
2. 코틀린에서는 `obj as Person`으로 타입 캐스팅한다. <br />
3. 코틀린에서는 if 문에서 타입 체크가 됐다면 따로 타입 캐스팅할 필요 없이 `스마트 캐스트`를 지원한다.
</td>
</tr>
</table>

### 3. 코틀린의 3가지 특이한 타입
#### 코틀린의 3가지 특이한 타입 1 : Any
- 자바의 Object 역할. (모든 객체의 최상위 타입)
- 모든 Primitive 타입의 최상위 타입도 Any이다.
- Any 자체로는 null을 포함할 수 없어 null을 포함하고 싶다면, Any?로 표현.
- Any에 equals/hashCode/toString 존재.

#### 코틀린의 3가지 특이한 타입 2 : Unit
- 자바의 void와 동일한 역할.
- 자바의 void와 다르게 Unit은 타입 인자로 사용 가능하다. (제네릭에서 void를 쓰려면 Void 타입을 사용해야 한다)
- 함수형 프로그래밍에서 Unit은 단 하나의 인스턴스만 갖는 타입을 의미. 즉, 코틀린의 Unit은 실제 존재하는 타입이라는 것을 표현

#### 코틀린의 3가지 특이한 타입 3 : Nothing
- 함수가 정상적으로 끝나지 않았다는 사실을 표현하는 역할.
- ex) 무조건 예외를 반환하는 함수/무한 루프 함수 등
- 사실 위와 같은 함수는 잘 작성하지 않기 때문에 Nothing도 거의 사용하지 않게 된다.
```kotlin
fun fail(message: String): Nothing {
    throw IllegalArgumentException(message)
}
```

### 4. String Interpolation, String indexing
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Main {
  public static void main(String[] args) {
    Person person = new Person("한영규", 100);
    String log = String.format("사람의 이름은 %s이고 나이는 %s세 입니다", person.getName(), person.getAge());
  }
}
```
```java
public class Main {
  public static void main(String[] args) {
    // 문자열의 특정 문자 가져오기
    String str = "ABCDE";
    char ch = str.charAt(1);
  }
}
```

</td>
<td>

```kotlin
fun main() {
  val person = Person("최태현", 100)
  val log = "사람의 이름은 ${person.name}이고 나이는 ${person.age}세 입니다"

  // $변수를 사용할 수도 있다.
  // 변수 이름만 사용할 수 있더라도 ${변수}를 사용하는 것이 가독성, 일괄 변환, 정규식 활용 측면에서 좋다.
  val name = "최태현"
  val age = 100
  val log = "사람의 이름: $name 나이: $age

  // 여러 줄에 걸친 문자열을 작성해야 할 때 큰 따옴표 3개(""" """)형식을 사용하면 깔끔하게 코딩하 ㄹ수 있다.
  val withoutIndent = """
    ABC
    123
    456
    ${name}
    $age
  """.trimIndent() // intellij에서 자동으로 trimIndent()를 추가해준다.

}
```
```kotlin
fun main() {
  // 문자열의 특정 문자 가져오기
  val str = "ABCDE"
  val ch = str[1]
}
```
</td>
</tr>
</table>

## Lec 04. 코틀린에서 연산자를 다루는 방법
### 1. 단항 연산자 / 산술 연산자
- 자바와 코틀린 완전 동일하다.

### 2. 비교 연산자와 동등성, 동일성
#### 비교 연산자
- 자바와 코틀린 사용법이 동일하다.
- 자바와 다르게, 코틀린에서는 객체를 비교할 때 비교 연산자를 사용하면 자동으로 `compareTo`를 호출해준다.
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Main {
  public static void main(String[] args) {
    JavaMoney money1 = new JavaMoney(1_000L);
    JavaMoney money2 = new JavaMoney(2_000L);
     
    if (money1.compareTo(money2) > 0) {
      System.out.println("Money1이 Money2보다 금액이 큽니다");
    }
  }
}

public class JavaMoney implements Comparable<JavaMoney> {
 
  private final long amount;
 
  public JavaMoney(long amount) {
    this.amount = amount;
  }
 
  public JavaMoney plus(JavaMoney other) {
    return new JavaMoney(this.amount + other.amount);
  }
 
  @Override
  public int compareTo(@NotNull JavaMoney o) {
    return Long.compare(this.amount, o.amount);
  }
 
  @Override
  public boolean equals(Object o) {
    if (this == o) return true;
    if (o == null || getClass() != o.getClass()) return false;
    JavaMoney javaMoney = (JavaMoney) o;
    return amount == javaMoney.amount;
  }
 
  @Override
  public int hashCode() {
    return Objects.hash(amount);
  }
 
  @Override
  public String toString() {
    return "JavaMoney{" +
        "amount=" + amount +
        '}';
  }
 
}
```

</td>
<td>

```kotlin
fun main() {
  val money1 = JavaMoney(2_000L)
  val money2 = JavaMoney(1_000L)
   
  if (money1 > money2) { // 코틀린에서는 비교 연산자 상황이 되면, 자동으로 compareTo를 자동으로 호출해준다.
      println("Money1이 Money2보다 금액이 큽니다")
  } 
}

```
</td>
</tr>
</table>

#### 동일성(Idenntity)과 동등성(Equality)
- 동일성 : 두 객체가 동일한 객체인가? 즉, 주소가 같은가
- 동등성 : 두 객체의 값이 같은가?

<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Main {
  public static void main(String[] args) {
    JavaMoney money1 = new JavaMoney(1_000L);
    JavaMoney money2 = money1;
    JavaMoney money3 = new JavaMoney(1_000L);
    
    System.out.println(money1 == money2); // true, 동일성
    System.out.println(money1 == money3); // false
    System.out.println(money1.equals(money3)); // true, 동등성
  }
}
```

</td>
<td>

```kotlin
fun main() {
  val money1 = JavaMoney(2_000L)
  val money2 = money1
  val money3 = JavaMoney(2_000L)
  
  println(money1 === money2) // ture, 동일성
  println(money1 === money3) // false
  println(money1 == money3) // ture, 동등성 
}

```
</td>
</tr>
<tr>
    <td>
        - 자바에서는 동일성에 ==을 사용하고, 동등성에 equals를 직접 호출 <br/>
    </td>
    <td>
        - 코틀린에서는 동일성에 ===을 사용하고, 동등성에 ==을 호출 -> ==을 사용하면 간접적으로 equals를 호출해준다. <br/>
</td>
</tr>
</table>

### 3. 논리 연산자 / 코틀린에 있는 특이한 연산자
#### 논리 연산자
- 자바와 코틀린이 완전히 동일하다.
- 자바처럼 코틀린에서도 Lazy 연산을 수행한다.

```kotlin
fun main() {
    if (fun1() || fun2()) { // fun1()이 true이므로, fun2()을 호출하지 않고 바로 "본문"을 출력한다. -> lazy 연산
        println("본문")
    }

    // 결과
    // fun1
    // 본문

    if(fun2() && fun1()) { // fun1()이 false이므로, fun1()을 호출하지 않고 바로 "본문"을 출력한다. -> lazy 연산
        println("본문")
    }

    // 결과
    // fun2
    // 본문

}
 
fun fun1(): Boolean {
    println("fun1")
    return true
}
 
fun fun2(): Boolean {
    println("fun2")
    return false
}

```

#### 코틀린에 있는 특이한 연산자
1. in / !in
- 컬렉션이나 범위에 포함되어 있다. 포함되어 있지 않다.
2. a..b
- a부터 b까지의 범위 객체를 생성한다.
3. a[i]
- a에서 특정 index i로 값을 가져온다.
```kotlin
val str = "ABC"
println(str[2]) // C
```
4. a[i] = b
- a에서 특정 index i에 b를 넣는다.


### 4. 연산자 오버로딩
- 코틀린에서는 객체마다 연산자를 직접 정의할 수 있다.
```kotlin
data class Money (
    val amount: Long
) {
    operator fun plus(other: Money): Money {
        return Money(this.amount + other.amount)
    }
}

fun main() {
    val money1 = Money(2_000L)
    val money2 = Money(1_000L)
    println(money1 + money2)
    
    // 결과
    Money(amount=3000)
}
```





## Lec 04. 코틀린에서 연산자를 다루는 방법
### 1. 단항 연산자 / 산술 연산자
- 자바와 코틀린 완전 동일하다.

### 2. 비교 연산자와 동등성, 동일성
#### 비교 연산자
- 자바와 코틀린 사용법이 동일하다.
- 자바와 다르게, 코틀린에서는 객체를 비교할 때 비교 연산자를 사용하면 자동으로 `compareTo`를 호출해준다.
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Main {
  public static void main(String[] args) {
    JavaMoney money1 = new JavaMoney(1_000L);
    JavaMoney money2 = new JavaMoney(2_000L);
     
    if (money1.compareTo(money2) > 0) {
      System.out.println("Money1이 Money2보다 금액이 큽니다");
    }
  }
}

public class JavaMoney implements Comparable<JavaMoney> {
 
  private final long amount;
 
  public JavaMoney(long amount) {
    this.amount = amount;
  }
 
  public JavaMoney plus(JavaMoney other) {
    return new JavaMoney(this.amount + other.amount);
  }
 
  @Override
  public int compareTo(@NotNull JavaMoney o) {
    return Long.compare(this.amount, o.amount);
  }
 
  @Override
  public boolean equals(Object o) {
    if (this == o) return true;
    if (o == null || getClass() != o.getClass()) return false;
    JavaMoney javaMoney = (JavaMoney) o;
    return amount == javaMoney.amount;
  }
 
  @Override
  public int hashCode() {
    return Objects.hash(amount);
  }
 
  @Override
  public String toString() {
    return "JavaMoney{" +
        "amount=" + amount +
        '}';
  }
 
}
```

</td>
<td>

```kotlin
fun main() {
  val money1 = JavaMoney(2_000L)
  val money2 = JavaMoney(1_000L)
   
  if (money1 > money2) { // 코틀린에서는 비교 연산자 상황이 되면, 자동으로 compareTo를 자동으로 호출해준다.
      println("Money1이 Money2보다 금액이 큽니다")
  } 
}

```
</td>
</tr>
</table>

#### 동일성(Idenntity)과 동등성(Equality)
- 동일성 : 두 객체가 동일한 객체인가? 즉, 주소가 같은가
- 동등성 : 두 객체의 값이 같은가?

<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Main {
  public static void main(String[] args) {
    JavaMoney money1 = new JavaMoney(1_000L);
    JavaMoney money2 = money1;
    JavaMoney money3 = new JavaMoney(1_000L);
    
    System.out.println(money1 == money2); // true, 동일성
    System.out.println(money1 == money3); // false
    System.out.println(money1.equals(money3)); // true, 동등성
  }
}
```

</td>
<td>

```kotlin
fun main() {
  val money1 = JavaMoney(2_000L)
  val money2 = money1
  val money3 = JavaMoney(2_000L)
  
  println(money1 === money2) // ture, 동일성
  println(money1 === money3) // false
  println(money1 == money3) // ture, 동등성 
}

```
</td>
</tr>
<tr>
    <td>
        - 자바에서는 동일성에 ==을 사용하고, 동등성에 equals를 직접 호출 <br/>
    </td>
    <td>
        - 코틀린에서는 동일성에 ===을 사용하고, 동등성에 ==을 호출 -> ==을 사용하면 간접적으로 equals를 호출해준다. <br/>
</td>
</tr>
</table>

### 3. 논리 연산자 / 코틀린에 있는 특이한 연산자
#### 논리 연산자
- 자바와 코틀린이 완전히 동일하다.
- 자바처럼 코틀린에서도 Lazy 연산을 수행한다.

```kotlin
fun main() {
    if (fun1() || fun2()) { // fun1()이 true이므로, fun2()을 호출하지 않고 바로 "본문"을 출력한다. -> lazy 연산
        println("본문")
    }

    // 결과
    // fun1
    // 본문

    if(fun2() && fun1()) { // fun1()이 false이므로, fun1()을 호출하지 않고 바로 "본문"을 출력한다. -> lazy 연산
        println("본문")
    }

    // 결과
    // fun2
    // 본문

}
 
fun fun1(): Boolean {
    println("fun1")
    return true
}
 
fun fun2(): Boolean {
    println("fun2")
    return false
}

```

#### 코틀린에 있는 특이한 연산자
1. in / !in
- 컬렉션이나 범위에 포함되어 있다. 포함되어 있지 않다.
2. a..b
- a부터 b까지의 범위 객체를 생성한다.
3. a[i]
- a에서 특정 index i로 값을 가져온다.
```kotlin
val str = "ABC"
println(str[2]) // C
```
4. a[i] = b
- a에서 특정 index i에 b를 넣는다.


### 4. 연산자 오버로딩
- 코틀린에서는 객체마다 연산자를 직접 정의할 수 있다.
```kotlin
data class Money (
    val amount: Long
) {
    operator fun plus(other: Money): Money {
        return Money(this.amount + other.amount)
    }
}

fun main() {
    val money1 = Money(2_000L)
    val money2 = Money(1_000L)
    println(money1 + money2)
    
    // 결과
    Money(amount=3000)
}
```






## Lec 05. 코틀린에서 조건문을 다루는 방법
### 1. if문
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Main {
    private void validateScoreIsNotNegative(int score) {
      if (score < 0) {
        throw new IllegalArgumentException(String.format("%s는 0보다 작을 수 없습니다.", score));
      }
    }
}
```
```java
public class Main {
  private String getPassOrFail(int score) {
    if (score >= 50) {
      return "P";
    } else {
      return "F";
    }
      
    // 30 + 40 = 70이라는 하나의 결과가 나온다. (Expression 이면서 Statement)
    int score = 30 + 40;

    // 컴파일 에러가 발생한다. 왜냐하면, 자바에서는 if 문을 하나의 값으로 취급하지 않기 떄문이다.
    // 따라서, 자바에서는 if-else가 Statement 이다.
    String grade = if (score >= 50) {
      "P";
    } else {
      "F";
    }

    // 단, 3항 연산자는 하나의 값으로 취급하므로, 컴파일 에러가 없다. (Expression 이면서 Statement)
    String grade = score >= 50 ? "P" : "F";
    
    // if - else if -else 문도 문법이 동일하다.
    private String getGrade(int score) {
      if (score >= 90) {
        return "A";
      } else if (score >= 80) {
        return "B";
      } else if (score >= 70) {
        return "C";
      } else {
        return "D";
      }
    }
  }
}
```
</td>
<td>

```kotlin
fun validateScoreIsNotNegative(score: Int) { // Unit(void)는 생략 가능
  if (score < 0) {
    throw IllegalArgumentException("${score}는 0보다 작을 수 없습니다")
  }
}
```

```kotlin
fun getPassOrFail1(score: Int): String {
    if (score >= 50) {
        return "P"
    } else {
        return "F"
    }
}

// 코틀린에서는 if-else 문이 Expressions이기 때문에, 하나의 값으로 취급할 수 있다. 따라서, 
fun getPassOrFail2(score: Int): String {
  return if (score >= 50) {
    "P"
  } else {
    "F"
  }
}

// if - else if - else 문도 문법이 동일하다.
fun getGrade(score: Int): String {
  if (score >= 90) {
    return "A"
  } else if (score >= 80) {
    return "B"
  } else if (score >= 70) {
    return "C"
  } else {
    return "D"
  }
}

// 코틀린에서는 return이 가장 앞에 오고 if - else if - else를 쭉 쓸 수 있다.  
fun getGrade(score: Int): String {
  return if (score >= 90) {
    "A"
  } else if (score >= 80) {
    "B"
  } else if (score >= 70) {
    "C"
  } else {
    "D"
  }
}

```
</td>
</tr>

<tr>
    <td>
        - 자바에서는 Exception을 던질 때 new를 사용해서 예외를 던졌습니다. <br/>
        - 자바에서는 if-else가 `Statement` 이다.
    </td>
    <td>
        - 코틀린에서는 Exception을 던질 때 new를 사용하지 않고 예외를 던졌습니다. <br/>
        - 코틀린에서는 if-else가 `Expression` 이다. 따라서, 3항 연산자가 없다.
</td>
</tr>
</table>



### 2. Expression 과 Statement
- Statement : 프로그램의 문장, 하나의 값으로 도출되지 않는다. <br/>
- Expression : 하나의 값으로 도출되는 문장 <br/>
- Expression은 Statement에 포함된다. <br/>
- 즉, Statement 중에 하나의 값으로 도출되는 문장들이 Expression 이다.


> 간단한 Tip <br />
> 어떠한 값이 특정 범위에 포함되어 있는지, 포함되어 있지 않은지 <br />
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Main {
    private void validateScore(int score) {
      if(0 <= score && score <= 100) {
        throw new IllegalArgumentException(String.format("%s는 0 <= score <= 100", score));
      }
    }
}
```

</td>
<td>

```kotlin
fun validateScore(score: Int) {
  if (score in 0..100) { // 포함되어 있는 경우 : score 값이 0부터 100 사이에 있다면, if 문 실행
    throw IllegalArgumentException("${score}는 0부터 100 사이에 있습니다.")
  }


  if (score !in 0..100) { // 포함되어 있지 않은 경우 : score 값이 0부터 100 사이에 있지 않으면, if 문 실행
    throw IllegalArgumentException("${score}는 0부터 100 사이에 있지 않습니다.")
  }
}
```
</td>
</tr>
</table>




### 3. switch 와 when
```
when(값) {
    // 조건부에는 어떠한 expression이라도 들어갈 수 있다. (예 : is Type)
    조건부 -> 어떠한 구문
    조건부 -> 어떠한 구문
    else -> 어떠한 굼누
}
```
- when 역시 Expression이기 때문에, when을 통해서 나온 결과를 바로 return 할 수 있다.
- 특정한 값이 특정한 값일 때, 분기를 칠 수 있다.
- 어떠한 범위에 있거나 혹은 다른 기타 조건을 사용해서, 분기를 칠 수 있다.

> when은 Enum Class 혹은 Sealed Class와 함께 사용할 경우, 더욱더 진가를 발휘한다.

> when 예시1 : when 문법의 조건부에는 어떠한 expression이라도 들어갈 수 있다. (예 : is Type)
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Main {
  private boolean startsWithA(Object obj) {
    if (obj instanceof String) {
      return (((String) obj).startsWith("A"));
    } else {
      return false;
    }
  }
}
```

</td>
<td>

```kotlin
fun startsWithA(obj: Any): Boolean { // 자바의 Object 대신 코틀린에서는 Any가 최상위 타입
  return when (obj) {
    is String -> obj.startsWith("A") // 스마트 캐스트
    else -> false
  }
}
```
</td>
</tr>
</table>

> when 예시 2 : when 문법의 조건문에는 여러 개의 조건을 동시에 검사할 수 있다. (`,`으로 구분)
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Main {
  private void judgeNumber(int number) {
    if (number == 1 || number == 0 || number == -1) {
      System.out.println("어디서 많이 본 숫자입니디");
    } else {
      System.out.println("1, 0, -1이 아닙니다");
    }
  }
}
```

</td>
<td>

```kotlin
fun judgeNumber(number: Int) {
  when (number) {
    1, 0, -1 -> println("어디서 많이 본 숫자입니다")
    else -> println("1, 0, -1이 아닙니다")
  }
}
```
</td>
</tr>
</table>

> when 예시 3 : when 문법의 값이 없을 수도 있다. - early retrun 처럼 동작
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Main {
  private void judgeNumber2(int number) {
    if (number == 0) {
      System.out.println("주어진 숫자는 0입니다");
      return;
    }

    if (number % 2 == 0) {
      System.out.println("주어진 숫자는 짝수입니다");
      return;
    }

    System.out.println("주어지는 숫자는 홀수입니다");
  }
}
```

</td>
<td>

```kotlin
fun judgeNumber2(number: Int) {
  when {
    number == 0 -> println("주어진 숫자는 0입니다")
    number % 2 == 0 -> println("주어진 숫자는 짝수입니다")
    else -> println("주어지는 숫자는 홀수입니다")
  }
}
```
</td>
</tr>
</table>

## Lec 06. 코틀린에서 반복문을 다루는 방법
### 1. for-each 문
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Main {
  public static void main(String[] args) {
    List<Long> numbers = Arrays.asList(1L, 2L, 3L);
    
    for (long number : numbers) { // 콜론(:)을 사용
      System.out.println(number);
    }
  }
}
```

</td>
<td>

```kotlin
fun main() {
  val numbers = listOf(1L, 2L, 3L)

  for (number in numbers) { // in을 사용, 
    println(number)
  }    
}

```
</td>
</tr>

<tr>
    <td>
        1. 자바에서는 컬렉션을 ~ 으로 만든다. <br/>
        2. 자바에서의 for-each문은 콜론(:)을 사용한다.
    </td>
    <td>
        1. 코틀린에서는 컬렉션을 ~ 으로 만든다. <br/>
        2. 코틀린에서의 for-each문은 `in`을 사용한다. in 뒤에는 자바와 동일하다. 즉, Iterable이 구현된 타입이라면 모두 들어갈 수 있다.
</td>
</tr>
</table>

### 2. 전통적인 for 문
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Main {
  public static void main(String[] args) {
    // 숫자가 1씩 증가하는 경우
    for (int i = 1; i <= 3; i++) {
      System.out.println(i);
    }
    
    // 숫자가 1씩 감소하는 경우
    for (int i = 3; i <= 1; i--) {
      System.out.println(i);
    }

    // 숫자가 2씩 증가하는 경우
    for (int i = 1; i <= 5; i += 2) {
      System.out.println(i);
    }
  }
}
```

</td>
<td>

```kotlin
fun main() {
  // 숫자가 1씩 증가하는 경우
  for (i in 1..3) { // 1부터 3까지
    println(i)
  }
  
  // 숫자가 1씩 감소하는 경우
  for (i in 3 downTo 1) {
    println(i)
  }

  // 숫자가 2씩 증가하는 경우
  for (i in 1..5 step 2) {
    println(i)
  }
}

```
</td>
</tr>
- downTo, step도 함수다.
- 코틀린에서 [변수.함수이름(argument)] 대신 [변수 함수이름 argument]로 호출하는 함수를 중위 함수라고 한다.

</table>


### 3. Progression과 Range
#### .. 연산자 -> 등차 수열(시작값, 끝값, 공차)을 만들어주는 연산자
- 범위를 만들어 내는 연산자
- 예시) 1..3 (1부터 3의 범위) : 1에서 시작하고 3으로 끝나는 등차수열을 만들어 줘



### 4. while 문
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Main {
  public static void main(String[] args) {
    int i = 1;
    
    while (i <= 3) {
      System.out.println(i);
      i++;
    }
  }
}
```

</td>
<td>

```kotlin
fun main() {
  var i = 1
  
  while (i <= 3) {
    println(i)
    i++
  }
}

```
</td>
</tr>
<tr>
- 자바와 코틀린 거의 동일
</tr>
</table>


## Lec 07. 코틀린에서 예외를 다루는 방법
### 1. try catch finally 구문
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Main {
  private void judgeNumber2(int number) {
    if (number == 0) {
      System.out.println("주어진 숫자는 0입니다");
      return;
    }

    if (number % 2 == 0) {
      System.out.println("주어진 숫자는 짝수입니다");
      return;
    }

    System.out.println("주어지는 숫자는 홀수입니다");
  }
}
```

</td>
<td>

```kotlin
fun judgeNumber2(number: Int) {
  when {
    number == 0 -> println("주어진 숫자는 0입니다")
    number % 2 == 0 -> println("주어진 숫자는 짝수입니다")
    else -> println("주어지는 숫자는 홀수입니다")
  }
}
```
</td>
</tr>
</table>

## Lec 06. 코틀린에서 반복문을 다루는 방법
### 1. for-each 문
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Main {
  private int parseIntOrThrow(@NotNull String str) {
    try {
      return Integer.parseInt(str);
    } catch (NumberFormatException e) {
      throw new IllegalArgumentException(String.format("주어진 %s는 숫자가 아닙니다", str));
    }
  }
  
  // 실패하면 Null을 반환해보자.
  private Integer parseIntOrThrowV2(String str) {
    try {
      return Integer.parseInt(str);
    } catch (NumberFormatException e) {
      return null;
    }
  }
}
```

</td>
<td>

```kotlin
fun parseIntOrThrow(str: String): Int {
    try { // try catch finally 구문은 문법적으로 동일하다.
      return str.toInt() // 기본 타입간의 형변환은 toType()을 사용한다.
    } catch (e: NumberFormatException) { // 타입이 뒤에 위치한다.
      throw IllegalArgumentException("주어진 ${str}는 숫자가 아닙니다") // `new`를 사용하지 않았다. 포맷팅이 간결하다.
    }
}

// 실패하면 Null을 반환해보자.
fun parseIntOrThrowV2(str: String): Int? { 
  try {
    return str.toInt()
  } catch (e: NumberFormatException) {
    return null
  }
}

// try catch도 코틀린에서 if문 처럼 하나의 Expression 처럼 간주된다.
fun parseIntOrThrowV2(str: String): Int? {
  return try {
    str.toInt()
  } catch (e: NumberFormatException) {
    null
  }
}

```
</td>
</tr>

<tr>
    <td>
        1. 자바에서는 
    </td>
    <td>
        1. 코틀린에서는 try   <br/>
</td>
</tr>
</table>

### 2. Checked Exception과 Unchecked Exception
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Main {
  // 프로젝트 내 파일의 내용물을 읽어오는 예제
  public void readFile() throws IOException {
    File currentFile = new File(".");
    File file = new File(currentFile.getAbsoluteFile() + "/a.txt");
    BufferedReader reader = new BufferedReader(new FileReader(file));
    System.out.println(reader.readLine());
    reader.close();
  }
}
```

</td>
<td>

```kotlin
fun readFile() { // throws 구문이 없다. 
  val currentFile = File(".")
  val file = File(currentFile.absolutePath + "/a.txt")
  val reader = BufferedReader(FileReader(file))
  println(reader.readLine())
  reader.close()
}
```
</td>
</tr>

<tr>
    <td>
        1. 자바에서는 IOException 같은 Checked Exception 이 발생할 경우, throws 를 해주어야 한다.
    </td>
    <td>
        1. 코틀린에서는 throws 구문이 없다. 
        - 그 이유는 코틀린에서는 Checked Exception과 Unchecked Exception을 구분하지 않는다. 모두 Unchecked Exception이다.  <br/>
        - 따라서, IOException 같은 Checked Exception 이 발생해도 throws를 해주지 않는다.
        - 단, Unckecked Exception으로 간주하는 것 뿐이지, 실제 동작은 자바에서와 동일하다.
        - 즉, IOException이 발생하면, 트랜잭션 롤백이 안되는 등 내부적으로는 Checked, Unchecked 구분이 필요하다.
</td>
</tr>
</table>




### 3. try with resources
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class Main {
  // 프로젝트 내 파일의 내용물을 읽어오는 예제
  public void readFile(String path) throws IOException {
    try (BufferedReader reader = new BufferedReader(new FileReader(path))) {
      System.out.println(reader.readLine());
    }
  }
}
```

</td>
<td>

```kotlin
fun readFile(path: String) {
  BufferedReader(FileReader(path)).use { reader ->
    println(reader.readLine())
  }
}
```
</td>
</tr>

<tr>
    <td>
        1. 자바에서는 
    </td>
    <td>
        1. 코틀린에서는 try with resources 구문이 없고, 대신 use라는 inline 확장함수를 사용한다.

</td>
</tr>
</table>


## Lec 08. 코틀린에서 함수를 다루는 방법
### 1. 함수 선언 문법

### 2. default parameter

### 3. named argument(parameter)
- builder를 직접 만들지 않고 builder의 장점처럼 명시적으로 매개변수의 이름을 기재해줘서 코드 이해를 높혀준다. 
- 단, 코틀린에서 자바 함수를 가져다 사용할 때는 named argument를 사용할 수 없다.
- 왜냐하면, 코틀린에서 자바코드를 쓸 때, JVM 상에서 Java가 바이트 코드로 변환됐을 때 parameter 이름을 보존하고 있지 않기 때문이다.

### 4. 같은 타입의 여러 파라미터 받기 (가변인자)
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public static void main(String[] args) {
  // 배열을 직접 넣거나, comma를 이용해 여러 파라미터를 넣는다
  String[] array = new String[]{"A", "B", "C"};
  printAll(array);
  printAll("A", "B", "C");
}
 
public static void printAll(String... strings) { // 타입 뒤에 (...)를 붙여준다. 
  for (String str : strings) {
    System.out.println(str);
  }
}
```

</td>
<td>

```kotlin
fun main() {
    val array = arrayOf("A", "B", "C")
    printAll(*array) // 배열을 바로 넣는대신 스프레드 연산자(*)를 붙여주어야 한다

    printAll("A", "B", "C")
}

fun printAll(vararg strings: String) { // vararg를 사용한다
    for (str in strings) {
        println(str)
    }
}
```
</td>
</tr>
</table>

## Lec 09. 코틀린에서 클래스를 다루는 방법
### 1. 클래스와 프로퍼티

- 프로퍼티 = 필드 + getter + setter
- 코틀린에서는 필드만 만들면, getter, setter를 자동으로 만들어준다.
- 코틀린에서 자바 클래스를 가져와 쓸 수 있는데, 그런 자바 클래스에 대해서도 .필드로 getter setter를 사용한다. 
- 
#### init
- 클래스가 초기화되는 시점에 한 번 호출되는 블록이다. 
- 값을 적절히 만들어주거나 validation 로직을 넣거나 하는 용도로 사용된다.
- 

### 2. 생성자와 init
#### 주생성자
- 주생성자의 특징은 반드시 존재해야 한다.
- 단, 주생성자에 파라미터가 하나도 없다면 생략 가능



#### 부생성자


- 코틀린에서는 부생성자보다는 default parameter를 권장한다.
- 즉, 파라미터를 넣어주지 않으면, 기본값을 쓰게 하는 것이다.
```kotlin

```


- 객체를 converting(어떤 객체를 다른 객체로 바꾸는 경우, ex. Ailen -> Person)하는 경우 부생성자를 사용할 수 있지만, 이 경우에는 정적 팩토리 메서드를 추천한다.







#### constructor
- 생성자 추가할 때 사용하는 키워드
- 

### 3. 커스텀 getter, setter


- 객체의 속성을 나타내는 거라면, custom getter를 사용하고, 그렇지 않다면 함수를 사용한다.
- Custom getter를 사용하면, 자기 자신을 변형해 줄 수도 있다.


- setter 자체를 지양하기 때문에, custom setter도 잘 안쓴다.
- 



### 4. backing field
- 무한루프를 막기 위한 예약어, 자기 자신을 가리킨다.
- 자기 자신을 가리키는 보이지 않는 field다 라고 해서, backing field라고 부른다.
- 강사의 개인적 경험상 custom getter에서 backing field를 쓰는 경우는 드물었다.
- 


### 요약
- 코틀린에서는 필드를 만들면 getter와 (필요에 따라) setter가 자동으로 생긴다. 때문에 이를 프로퍼티라고 부른다.
- 코틀린에서는 주생성자가 필수이다.
- 코틀린에서는 constructor 키워드를 사용해 부생성자를 추가로 만들 수 있다.
- 단, default parameter나 정적 팩토리 메소드를 추천한다.
- 실제 메모리에 존재하는 것과 무관하게 custom getter와 custom setter를 만들 수 있다.
- custom getter, custom setter에서 무한루프를 막기 위해 `field`라는 키워드를 사용한다. 이를 `backing field`라고 부른다.


## Lec 10. 코틀린에서 상속을 다루는 방법
### 1. 추상 클래스
- 자바와 코틀린 모두 추상클래스는 인스턴스화할 수 없다.
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public abstract class JavaAnimal {

  protected final String species;
  protected final int legCount;

  public JavaAnimal(String species, int legCount) {
    this.species = species;
    this.legCount = legCount;
  }

  abstract public void move();

  public String getSpecies() {
    return species;
  }

  public int getLegCount() {
    return legCount;
  }

}
```
- Cat

```java
public class JavaCat extends JavaAnimal {
 
  public JavaCat(String species) {
    super(species, 4);
  }
 
  @Override
  public void move() {
    System.out.println("고양이가 사뿐 사뿐 걸어가~");
  }
 
}
```
- Penguin
```java
public final class JavaPenguin extends JavaAnimal {

  private final int wingCount;

  public JavaPenguin(String species) {
    super(species, 2);
    this.wingCount = 2;
  }

  @Override
  public void move() {
    System.out.println("펭귄이 움직입니다~ 꿱꿱");
  }

  @Override
  public int getLegCount() {
    return super.legCount + this.wingCount;
  }

}
```

</td>
<td>

```kotlin
abstract class Animal(
    protected val species: String,
    protected open val legCount: Int, // 프로퍼티를 override 할 때, 추상 프로퍼티가 아니라면 상속 받을 때 무조건 Open을 붙여줘야만 한다.
) {
    abstract fun move()
}
```
- Cat
```kotlin
class Cat(
    species: String,
) : Animal(species, 4) { // 상위 클래스의 생성자를 바로 호출한다
    
    override fun move() { // override를 필수적으로 붙여 주어야 한다
        println("고양이가 사뿐 사뿐 걸어가~")
    }
}
```
- Penguin
```kotlin
class Penguin(
    species: String,
) : Animal(species, 2) {
 
    private val wingCount: Int = 2
 
    override fun move() {
        println("펭귄이 움직인다~ 꽥꽥")
    }
 
    override val legCount: Int
        get() = super.legCount + this. wingCount
 
}
```



</td>
</tr>

<tr>
    <td>
        1. 자바에서는 
    </td>
    <td>
        1. 코틀린에서는 

</td>
</tr>
</table>


### 2. 인터페이스
- 자바, 코틀린 모두 인터페이스를 인스턴스화 할 수 없다.


<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public interface JavaFlyable {

  default void act() {
    System.out.println("파닥 파닥");
  }
  
  // 인터페이스에 추상 메서드도 넣을 수 있다.
  void fly();
}
```

```java
public interface JavaSwimable {

  default void act() {
    System.out.println("어푸 어푸");
  }
}
```

```java
public final class JavaPenguin extends JavaAnimal implements JavaSwimable, JavaFlyable {
 
  // ...
  @Override
  public void act() {
    JavaSwimable.super.act();
    JavaFlyable.super.act();
  }
 
}
```
</td>
<td>

```kotlin
interface Flyable {
  fun act() { // 코틀린은 default 키워드 없이 기본 메서드 구현이 가능하다.
    println("파닥 파닥")
  }
  
  // 디폴트 메소드 구현시, default 키워드 없이 가능하다.
  fun fly()
  
}
```

```kotlin
interface Swimable {
    
  // 코틀린에서는 backing field 가 없는 프로퍼티를 interface에 만들 수 있다.
  val swimAbility: Int
//    get() = 3 : 인터페이스에서 값을 넣어줘도 됨. 
    
  fun act() {
    println(swimAbility)

    println("어푸 어푸")
  }
}
```

```kotlin
class Penguin(
    species: String,
) : Animal(species, 2), Swimable, Flyable { // 인터페이스 구현도 콜론(:)을 사용한다.
 
    // ...
 
    override fun act() {
        super<Swimable>.act() // 중복되는 인터페이스를 특정할 때 super<타입>.함수 사용
        super<Flyable>.act()
    }
  
  override val swimAbility: Int
    get() = 3
 
}
```


</td>
</tr>

<tr>
    <td>
        1. 자바에서는 
    </td>
    <td>
        1. 코틀린에서는 

</td>
</tr>
</table>




### 3. 클래스를 상속할 때 주의할 점
```kotlin
// 부모 클래스의 추상 프로퍼티가 아닌 프로퍼티에는 open을, 자식 클래스에는 해당 프로퍼티에 override를 붙여야 한다.
open class Base( // Base 클래스를 다른 클래스가 상속받을 수 있게 open으로 열어줌
    open val number: Int = 100, // number 라는 프로퍼티를 누군가가 override 할 수 있게끔 open으로 열어줌
) {
    init {
        println("Base Class")
        println(number)
    }
}
```

```kotlin
class Derived(
    override val number: Int,
) : Base(number) {
    init {
        println("Derived Class")
    }
}
```

- 상위 클래스를 설계할 때, 생성자 또는 초기화 블록에 사용되는 프로퍼티에는 open을 피해야 한다.
```kotlin
fun main() {
    Derived(300) // Derived() 생성자를 호출하면 어떤 값이 찍힐까?
}

// 결과
// Base Class
// 0
// Derived Class

// 과정
// 1. Derieved()에서 Base() 호출
// 2. Base()의 초기화 블록에서 "Base Class" 출력
// 3. Base()의 초기화 블록에서 number 출력
// 4. 이 때 number는 Derived의 number인데 아직 Derived의 초기화 블록이 실행되지 않았기 때문에 Int 기본값인 0을 출력한다.
// 5. Derieved()의 초기화ㅣ 블록에서 "Derived Class" 출력

// 해당 결과는 number가 Derieved()인자인 300도 아닌, 부모 클래스의 기본값인 100도 아닌 0이 찍히므로, 의도한대로 동작하지 않았을 확률이 높다.
// 따라서, 상위 클래스를 설계할 때 생성자 또는 초기화 블록에 사용되는 프로퍼티는 open을 피해야 한다.
// 왜냐하면, 부모 클래스에서 open으로 특정 필드를 열어 놓으면 자식 클래스에서 override할 가능성을 열어 놓는 것이고, 해당 open 프로퍼티를 부모의 초기화 블럭에서 사용하게 되면 위 예시처럼 부모의 초기화 블록에서 자식의 프로퍼티를 사용함으로써 정상적으로 동작하지 않을 수 있다.
// 즉, 부모의 초기화 블록에서 사용할 프로퍼티는 open을 피함으로써, 자식이 상속받는 것을 방지해 의도한 대로 동작할 것을 기대할 수 있다.



```

### 4. 상속 관련 지시어 정리
#### 1. final 
- override를 할 수 없게 한다. 라는 의미
- default로 보이지 않게 존재한다.

#### 2. open
- override를 열어준다. 라는 의미

#### 3. abstract
- 반드시 override 해야 한다. 라는 의미

#### 4. override
- 상위 타입을 오버라이드 하고 있다. 라는 의미


### 요약
- 상속 또는 구현을 할 때에 : 를 사용해야 한다.
- 상위 클래스 상속을 구현할 때 생성자를 반드시 호출해야 한다. 
- override를 필수로 붙여야 한다. 
- 추상 멤버가 아니면 기본적으로 오버라이드가 불가능하다.
  - open을 사용해야 한다.
- 상위 클래스의 생성자 또는 초기화 블록에서 open 프로퍼티를 사용하면 얘기치 못한 버그가 생길 수 있다.


## Lec 11. 코틀린에서 접근 제어를 다루는 방법
### 1. 자바와 코틀린의 가시성 제어 
<img width="643" alt="스크린샷 2024-02-17 오후 8 47 22" src="https://github.com/daadaadaah/my-java/assets/60481383/038f6eb1-0d29-4354-acab-d552c2564781">

- 코틀린에서는 패키지를 namespace를 관리하기 위한 용도로만 사용하고, 가시성 제어에는 사용되지 않는다.
- 자바의 기본 접근 지시어는 `default`, 코틀린의 기본 접근 지시어는 `public` 이다.
- 코트린은 .kt 파일에 변수, 함수, 클래스 여러개를 바로 만들 수 있다.


### 2. 코틀린 파일의 접근 제어
<img width="275" alt="스크린샷 2024-02-17 오후 8 53 41" src="https://github.com/daadaadaah/my-java/assets/60481383/4fb9df90-b411-4b21-8909-cf8ec38f4b5c">
- protected 사용 불가능한 이유는 protected가 코틀린에서는 선정된 클래스와 하위 클래스에 작동하는 지시어인데, 클래스가 아니라 파일이므로,


### 3. 다양한 구성요소(클래스, 생성자, 프로퍼티)의 접근 제어
#### (1) 클래스
- 클래스 안의 멤버
![스크린샷 2024-02-17 오후 9.46.03.png](..%2F..%2F..%2F..%2F..%2Fvar%2Ffolders%2F4k%2Fr1d7r9ps1k9gnxnmj02gfhym0000gn%2FT%2FTemporaryItems%2FNSIRD_screencaptureui_ZBLTNM%2F%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202024-02-17%20%EC%98%A4%ED%9B%84%209.46.03.png)

#### (2) 생성자
- 생성자도 가시성 범위는 멤버와 동일하다.
- 단, 생성자에 접근 지시어를 붙이려면, constructor를 써줘야 한다.
```kotlin
class Cat internal constructor(
)
```

<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public abstract class StringUtils {
 
  private StringUtils() {}
 
  public boolean isDirectoryPath(String path) {
    return path.endsWith("/");
  }
}
```

</td>
<td>

```kotlin
// StringUtil.kt
fun isDirectoryPath(path: String): Boolean {
  return path.endsWith("/")
}
```
</td>
</tr>

<tr>
    <td>
        1. 자바에서는 유틸성 코드를 만들 때, abstract class + private contructor를 사용해서 인스턴스화를 막을 때가 있다.
    </td>
    <td>
        1. 코틀린에서는 코틀린도 비슷하게 가능하지만, 그냥 파일 최상단에 바로 유틸함수를 작성하면 편하다.
</td>
</tr>
</table>




#### (3) 프로퍼티
- 프로퍼티도 가시성 범위는 동일하다.
- 단, 프로퍼티의 가시성을 제어하는 방법으로는 2가지가 있다.
```kotlin
class Car(
    // 방법 1. getter, setter 한 번에 접근 지시어를 정하거나
    internal val name: String, // name에 대한 getter를 internal로 만들고 싶을 때
    var owner: String, // owner에 대한 getter와 setter를 private로 만들고 싶을 때
    _price: Int
) {
    var price = _price
        private set // 방법 2. getter 혹은 setter에만 추가로 가시성을 부여할 수 있다.
}
```


### 4. 자바와 코틀린을 함께 사용할 경우 주의할 점
1. Internal은 바이트 코드상 public이 된다. 따라서, 자바 코드에서는 코틀린 모듈의 internal 코드를 가져올 수 있다.
2. 자바의 protected와 코틀린에서의 protected는 다르다. 자바에서 코틀린 코드를 가져다 쓸 때, 같은 패키지의 코틀린 protected 멤버에 접근할 수 있다.
- 즉, 코틀린의 internal과 protected는 코틀린 내에서만 유효하다

### 요약
- Kotlin에서 패키지는 namespace 관리용이기 때문에 protected의 의미가 달라졌다.
- Kotlin에서는 default의 의미가 사라지고, 모듈간의 접근을 통제하는 internal이 새로 생겼다.
- 생성자에 접근 지시어를 붙일 때는 constructor를 명시적으로 써주어야 한다.
- 유틸성 함수를 만들 떄는 파일 최상단을 이용하면 편리하다.
- 프로퍼티의 custom setter에 접근 지시어를 붙일 수 있다.
- Java에서 Kotlin 코드를 사용할 때 internal과 protected는 주의해야 한다.


## Lec 12. 코틀린에서 object 키워드를 다루는 방법
### object 키워드가 사용되는 경우 1. static 함수와 변수
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class JavaPerson {

  private static final int MIN_AGE = 1;

  public static JavaPerson newBaby(String name) {
    return new JavaPerson(name, MIN_AGE);
  }

  private String name;

  private int age;

  private JavaPerson(String name, int age) {
    this.name = name;
    this.age = age;
  }

}
```

</td>
<td>

```kotlin
class Person private constructor(
  private val name: String,
  private val age: Int,
) {
  companion object {
    private const val MIN_AGE = 1

    fun newBaby(name: String): Person {
      return Person(name, MIN_AGE)
    }
  }
}
```
</td>
</tr>

<tr>
    <td>
        1. 자바에서는 유틸성 코드를 만들 때, abstract class + private contructor를 사용해서 인스턴스화를 막을 때가 있다.
    </td>
    <td>
        1. 코틀린에는 static이라는 키워드 자체가 없고, 대신에 companion object 블록 안에 넣어둔 변수와 함수가 자바의 static 변수와 함수인 것처럼 사용된다. 
</td>
</tr>
</table>

#### static :


#### companion object
- 클래스와 동행하는 유일한 오브젝트
- companion object, 즉 동반 객체도 하나의 객체로 간주된다.
- 때문에 이름을 붙일 수 있고, interface를 구현할 수도 있다.
```kotlin
interface Log {
    fun log()
}
```

```kotlin
class Person private constructor(
  private val name: String,
  private val age: Int,
) { 
    // Factory라는 이름을 붙이고, Log라는 인터페이스를 구현했다.
  companion object Factory : Log {
    private const val MIN_AGE = 1

    fun newBaby(name: String): Person {
      return Person(name, MIN_AGE)
    }

    override fun log() {
      println("LOG")
    }
  }
}
```
- companion object에 유틸성 함수들을 넣어도 되지만, 최상단 파일을 활용하는 것을 추천한다.


> 자바에서 코틀린에 있는 static field나 static 함수를 사용하고 싶을 때
#### 방법 1. 이름이 없으면 기본적으로 Companion을 사용한다
```kotlin
class Person private constructor(
    private val name: String,
    private val age: Int,
) {
    companion object { // companion object에 이름이 없을 때
        private const val MIN_AGE = 1
 
        fun newBaby(name: String): Person {
            return Person(name, MIN_AGE)
        }
    }
}
```
```java
// 자바에서 사용시
Person.Companion.newBaby("ABC");
```

#### 방법 2. 만약 companion object 이름이 있으면, 이름을 사용하면 된다.
```kotlin
class Person private constructor(
  private val name: String,
  private val age: Int,
) { 
  companion object Factory {
    private const val MIN_AGE = 1

    fun newBaby(name: String): Person {
      return Person(name, MIN_AGE)
    }
  }
}
```
```java
// 자바에서 사용시 
Person.Factory.newBaby("ABC");
```

#### 방법 3. 코틀린 코드에 @JvmStatic 붙이기
```kotlin
class Person private constructor(
    private val name: String,
    private val age: Int,
) {
    companion object {
        private const val MIN_AGE = 1
 
        @JvmStatic // 추가
        fun newBaby(name: String): Person {
            return Person(name, MIN_AGE)
        }
    }
}
```
```java
// 자바에서 사용시, 자바의 static field나 static 함수를 쓰는 것처럼 사용할 수 있다.
Person.newBaby("ABC");
```

#### const
- `val` 이라고 선언된 변수는 원래 런타임시에 변수가 할당되는데, `const`를 붙이게 되면, 컴파일 시에 변수가 할당된다.
- 진짜 상수에 붙이기 위한 용도로, 기본 타입과 String에 붙일 수 있음


### object 키워드가 사용되는 경우 2. 싱글톤
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class JavaSingleton {

  private static final JavaSingleton INSTANCE = new JavaSingleton();

  private JavaSingleton() { }

  public static JavaSingleton getInstance() {
    return INSTANCE;
  }

}
```

</td>
<td>

```kotlin
object Singleton

// 예시
object Singleton {
  var a: Int = 0
}

fun main() {
  println(Singleton.a) // 결과 : 0
  Singleton.a = 10
  println(Singleton.a) // 결과 : 10
}

```
</td>
</tr>

<tr>
    <td>
        1. 자바에서는 유틸성 코드를 만들 때, abstract class + private contructor를 사용해서 인스턴스화를 막을 때가 있다.
    </td>
    <td>
        1. 코틀린에는 static이라는 키워드 자체가 없고, 대신에 companion object 블록 안에 넣어둔 변수와 함수가 자바의 static 변수와 함수인 것처럼 사용된다. 
</td>
</tr>
</table>

### object 키워드가 사용되는 경우 3. 익명 클래스
- 익명 클래스 : 특정 인터페이스나 클래스를 상속받은 구현체를 1회성으로 사용할 때 쓰는 클래스

<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public interface Movable {
  void move();
  void fly();
}
```

```java
public static void main(String[] args) {
  moveSomething(new Movable() {
    @Override
    public void move() {
      System.out.println("움직인다~~");
    }
 
    @Override
    public void fly() {
	  System.out.println("난다~~");
    }
  });
}
 
private static void moveSomething(Movable movable) {
  movable.move();
  movable.fly();
}
```



</td>
<td>

```java
// 자바
public interface Movable {
  void move();
  void fly();
}
```
```kotlin
fun main() {
  moveSomething(object : Movable {
    override fun move() {
      println("움직인다")
    }

    override fun fly() {
      println("난다~~")
    }

  })
}

private fun moveSomething(movable: Movable) {
  movable.move()
  movable.fly()
}
```
</td>
</tr>

<tr>
    <td>
        1. 자바에서는 `new 타입이름()` 
    </td>
    <td>
        1. 코틀린에는 `object: 타입이름`
</td>
</tr>
</table>

### 요약
- Java의 static 변수와 함수를 만드려면, Kotlin에서는 companion object를 사용해야 한다.
- companion object도 하나의 객체로 간주되기 때문에 이름을 붙일 수 있고, 다른 타입을 상속받을 수도 있다.
- Kotlin에서 싱글톤 클래스를 만들 때 object 키워드를 사용한다.
- Kotlin에서 익명 클래스를 만들 때 object : 타입을 사용한다.


## Lec 13. 코틀린에서 중첩 클래스를 다루는 방법
> 서버 개발을 진행하면서 클래스 안에 클래스를 중첩해서 쓸 일이 별로 없다.
> 어떤 클래스간의 계층 관계를 나타내거나 논리적인 구조를 표현할 때 간혹 사용된다.


### 1. 중첩 클래스의 종류
- 중첩 클래스는 크게 2가지 종류가 있다
1. static을 사용하는 클래스
2. static을 사용하지 않는 클래스
   1) 내부 클래스(Inner Class)

   2) 지역 클래스(Local Class) 
   - 메소드 내부에 클래스를 정의한 것

   3) 익명 클래스(Anonymous Class)


### 2. 코틀린의 중첩 클래스와 내부 클래스
![스크린샷 2024-02-19 오후 3.06.59.png](..%2F..%2F..%2F..%2F..%2Fvar%2Ffolders%2F4k%2Fr1d7r9ps1k9gnxnmj02gfhym0000gn%2FT%2FTemporaryItems%2FNSIRD_screencaptureui_QaDJvO%2F%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202024-02-19%20%EC%98%A4%ED%9B%84%203.06.59.png)

> 코틀린에서는 이러한 가이드를 충실히 따르고 있다. 
> 의미 : 기본적으로 바깥 클래스를 참조하지 않는다. 만약, 바깥 클래스를 참조하고 싶다면, inner 키워드를 추가한다.

#### (1) 권장되는 중첩 클래스
```kotlin
class House(
    private var address: String,
    private var livingRoom: LivingRoom = LivingRoom(10.0)
) {
    class LivingRoom(
        private var area: Double,
    )
}
```
- 코틀린은 기본적으로 바깥 클래스에 대한 연결이 없는 중첩 클래스가 만들어진다.


#### (2) 권장되지 않는 중첩 클래스
```kotlin
class House(
    private var address: String,
) {
    private var livingRoom: LivingRoom = this.LivingRoom(10.0)
    
    inner class LivingRoom( // 중첩 클래스에서 바깥 클래스를 참조하고 싶다면, 중첩 클래스에 inner 키워드를 붙이면 된다.
      private var area: Double,
    ) {
        val address: String
            get() = this@House.address //  이 때, 자바와 다른 점은 바깥 클래스 참조를 위해 "this@바깥클래스"를 사용한다.
    }
}
```
### 요약
- 클래스 안에 클래스가 있는 경우 종류는 2가지였다.
  1. (Java 기준) static을 사용하는 클래스
  2. (Java 기준) static을 사용하지 않는 클래스
- 권장되는 클래스는 static을 사용하는 클래스이다.
- 코틀린에서는 이러한 가이드를 따르기 위해
  - 클래스 안에 기본 클래스를 사용하면 바깥 클래스에 대한 참조가 없고
  - 바깥 클래스를 참조하고 싶다면, inner 키워드를 붙여야 한다.
- 코틀린 inner class에서 바깥 클래스를 참조하려면 `this@바깥클래스`를 사용해야 한다.



## Lec 14. 코틀린에서 다양한 클래스를 다루는 방법
### 1. Data Class
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public class JavaPersonDto {

  private final String name;
  private final int age;

  public JavaPersonDto(String name, int age) {
    this.name = name;
    this.age = age;
  }

  public String getName() {
    return name;
  }

  public int getAge() {
    return age;
  }

  @Override
  public boolean equals(Object o) {
    if (this == o) return true;
    if (o == null || getClass() != o.getClass()) return false;
    JavaPersonDto that = (JavaPersonDto) o;
    return age == that.age && Objects.equals(name, that.name);
  }

  @Override
  public int hashCode() {
    return Objects.hash(name, age);
  }

  @Override
  public String toString() {
    return "JavaPersonDto{" +
            "name='" + name + '\'' +
            ", age=" + age +
            '}';
  }
}
```

</td>
<td>

```kotlin
data class PersonDto(
  val name: String,
  val age: Int,
)
```
</td>
</tr>

<tr>
    <td>
        1. 자바에서는 필드, 생성자, getter, equals, hashCode, toString을 정의한다. IDE를 활용할 수도 있고, lombok을 활용할 수도 있지만, 클래스가 장황해지거나, 클래스 생성 이후 추가적인 처리를 해줘야 하는 단점이 있다. 자바에서는 JDK 16부터 코틀린의 data class 같은 record class를 도입했다.
    </td>
    <td>
        1. 코틀린에는 class 앞에 data 키워드를 붙여주면 eqauls, hashCode, toString을 자동으로 만들어준다. 여기에 named argument까지 활용하면, builder pattern을 쓰는 것 같은 효과도 있다.
  </td>
</tr>
</table>


### 2. Enum Class
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
public enum JavaCountry {

  KOREA("KO"),
  AMERICA("US"),
  ;

  private final String code;

  JavaCountry(String code) {
    this.code = code;
  }

  public String getCode() {
    return code;
  }

}
```

</td>
<td>

```kotlin
enum class Country(
  private val code: String,
) {
  KOREA("ko"),
  AMERICA("US"),
  ;
}
```
</td>
</tr>

<tr>
    <td>
        1. 자바에서는 추가적인 클래스를 상속받을 수 없다. 인터페이스는 구현할 수 있으며, 각 코드가 싱글톤이다.
    </td>
    <td>
        1. 코틀린에서는 
  </td>
</tr>
</table>

> when을 enum class, sealed class와 함께 사용할 경우 더욱 진가를 발휘한다.
<table>
<tr>
  <td>Java</td>
  <td>kotlin</td>
</tr>

<tr>
<td>

```java
private static void handleCountry(JavaCountry country) {
    if (country == JavaCountry.KOREA) {
      // 로직 처리
    }
 
    if (country == JavaCountry.AMERICA) {
      // 로직 처리
    }
}
```


</td>
<td>

```kotlin
fun handleCountry(country: Country) {
  when (country) {
    Country.KOREA -> TODO()
    Country.AMERICA -> TODO()
  }
}
```
</td>
</tr>

<tr>
    <td>
        1. 코드가 많아지면 else 로직 처리 등 복잡도가 증가한다.
    </td>
    <td>
        1. 코틀린에서는 코틀린의 when을 사용하면 조금 더 읽기 쉬운 코드가 만들어진다. 또한, 컴파일러가 country의 모든 타입을 알고 있어서 else 로직을 작성하지 않아도 된다. 또한, Enum에 변화가 있으면 IDE 단에서 warning을 주는 식으로 알려준다.
    </td>
</tr>
</table>


### 3. Sealed Class, Sealed Interface
- 상속이 가능하도록 추상클래스로 만들까 하는데, 외부에서는 이 클래스를 상속받지 않았으면 좋겠어. 하위 클래스를 봉인하자 라는 의미에서 sealed class가 나왔다.
- sealed class의 이론적 특징은 다음과 같다.
  1. 컴파일 타임 때 하위 클래스의 타입을 모두 기억한다. 즉, 런타임때 클래스 타입이 추가될 수 없다. -> Enum과 같은 특성
  2. 하위 클래스는 sealed class와 같은 패키지에 있어야 한다.
- Enum과 다른 점은 다음과 같다. 
  1. 클래스를 상속받을 수 없는 Enum과 달리, 클래스를 상속받을 수 있다.
  2. 코드 하나하나가 싱글톤으로 단일 인스턴스를 가지고 있었던 Enum과 달리, 하위 클래스는 멀티 인스턴스가 가능하다.

> 추상화가 필요한 Entity 또는 DTO에 sealed class를 활용함
> 추가로, JDK 17에서도 Sealed class가 추가되었음 (단, 문법이 좀 다르다.)


### 요약
- Kotlin의 Data class를 사용하면 equals, hashCode, toString을 자동으로 만들어준다.
- Kotlin의 Enum Class는 Java의 Enum Class와 동일하지만, when과 함께 사용함으로써 큰 장점을 갖게 된다.
- Enum Class보다 유연하지만, 하위 클래스를 제한하는 Sealed Class 역시 when과 함께 주로 사용된다.



# Reference
- https://gksdudrb922.tistory.com/261
- https://velog.io/@paki1019/%EC%9E%90%EB%B0%94-%EA%B0%9C%EB%B0%9C%EC%9E%90%EB%A5%BC-%EC%9C%84%ED%95%9C-%EC%BD%94%ED%8B%80%EB%A6%B0-%EC%9E%85%EB%AC%B8Java-to-Kotlin-Starter-Guide
