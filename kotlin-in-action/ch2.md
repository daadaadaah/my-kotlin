# 2장. 코틀린 기초
## 2.1 기본 요소 : 함수와 변수
### 2.1.1 Hello, World!

### 2.1.2 함수

### 2.1.3 변수

### 2.1.4 더 쉽게 문자열 형식 지정 : 문자열 템플릿


## 2.2 클래스와 프로퍼티

### 2.2.1 프로퍼티

### 2.2.2 커스텀 접근자


```kotlin
class Rectangle(val height: Int, val width: Int) {
    val isSquare: Boolean
        get() {
            return height == width
        }
}

// get 간단 버전
class Rectangle(val height: Int, val width: Int) {
    val isSquare: Boolean
    	get() = height == width        
}

fun main(args: Array<String>) {
    
    val rectangle = Rectangle(41, 43)
    println("정사각형 인가요? : ${rectangle.isSquare}") // 정사각형 인가요? : false
}
```






### 2.2.3 코틀린 소스코드 구조 : 디렉터리와 패키지

## 2.3 선택 표현과 처리 : enum과 when

### 2.3.1 enum 클래스 정의

### 2.3.2 when으로 enum 클래스 다루기

### 2.3.3 when과 임의의 객체를 함께 사용

### 2.3.4 인자 없는 when 사용

### 2.3.5 스마트 캐스트 : 타입 검사와 타입 캐스트를 조합

### 2.3.6 리팩토링 : if를 when으로 변경

### 2.3.7 if와 when의 분기에서 블록 사용


## 2.4 대상을 이터레이션 : while과 for 루프
### 2.4.1 while 루프

### 2.4.2 수에 대한 이터레이션 : 범위와 수열

### 2.4.3 맵에 대한 이터레이션

### 2.4.4 in으로 컬렉션이나 범위의 원소 검사

## 2.5 코틀린의 예외 처리
### 2.5.1 try, catch, finally

### 2.5.2 try를 식으로 사용

## 2.6 요약
