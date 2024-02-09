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




# Reference
- https://gksdudrb922.tistory.com/261
- https://velog.io/@paki1019/%EC%9E%90%EB%B0%94-%EA%B0%9C%EB%B0%9C%EC%9E%90%EB%A5%BC-%EC%9C%84%ED%95%9C-%EC%BD%94%ED%8B%80%EB%A6%B0-%EC%9E%85%EB%AC%B8Java-to-Kotlin-Starter-Guide