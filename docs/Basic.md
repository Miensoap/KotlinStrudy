# Kotlin

## 특징💡

### 상호 운용성

코틀린은 자바와의 `상호운용성` 을 가진다.  
기존 자바 라이브러리와 완벽히 호환되며, 단일 프로젝트에서 일부는 자바, 일부는 코틀린으로 작성해도 문제가 없다.  

### Null Safety

코틀린은 언어 차원에서 `널 안정성` 을 지원한다.   
다음과 같이 `null` 허용 여부를 구분 가능하다.

```kotlin
fun stLen(s: String?) : Int{
    return if(s==null) 0 else s.length
}
```
> 위 예제 코드를 작성하며 발견한 것.  
> `s == null ? 0 : s.length();` 코드에서 오류가 발생했다.  
>   
> **코틀린은 `삼항 연산자` 를 지원하지 않으며, 대신 `if else` 가 표현식으로 사용된다.**


## 기본 문법💡

### 변수
`var` 키워드로 선언하고, 뒤이어 변수명과 타입을 작성한다.  
타입 추론이 가능해, 선언시 타입을 정하지 않아도 된다.

```java
//자바
int result = square(5);
```
```kotlin
var result: Int = square(5)
```

`val` 키워드로 자바의 `final` 기능을 사용할 수 있다.

### 자료형
모든 자료형을 참조형으로 제공한다.  
`Integer` - `Int`, `Character` - `Char` 로 대응된다.

실제로 컴파일될 때는 자바의 원시형과 동일한 바이트 코드를 사용해 속도를 최적화한다.  
참조형처럼 보이지만, 실제로는 외부 패키지를 대신 호출해 편의를 제공하는 기능이다.  

예를들어, `a.max()` 를 호출하면 `kotlin.collections.ArraysKt.max()` 를 호출한다.  

### 컬렉션 프레임워크

상호 운용성을 위해 자체 컬렉션을 구현하지 않고, 자바 컬렉션 프레임워크를 사용하며,  
리스트는 `ArrayList`를, 맵은 `LinkedHashMap` 을 기본 자료형으로 사용한다.

#### 확장 함수 사용
```kotlin
val list = arrayListOf(1, 2, 3)
list.javaClass // java.util.ArrayList
list.max()
```
위와 같이 `확장 함수` 기능을 이용해 `max()` 를 호출할 수 있도록 구현했다.

#### 불변성
코틀린에서 컬렉션은 기본적으로 불변이고, `Mutable` 이 붙은 별도의 인터페이스를 제공한다.

---

### 함수
선언에 `fun` 키워드를 사용한다.  
리턴 타입은 맨 뒤에 선언한다. (생략 가능)  
파라미터 타입 또한 파라미터 뒤에 선언한다.

```java
// 자바
public int square (int x) {}
```
```kotlin
// 코틀린
fun square(x: Int): Int {}
```

파타미터에 디폴트 값을 설정해, `메서드 오버로딩` 을 사용할 수 있다.  
또한, `Named Argument` 를 지원한다. 
> 자바에서는 이 기능이 존재하지 않아서 `빌더 패턴` 을 사용
```kotlin
fun overloadFun(paramA: Int, paramB: Int, paramC: Int = 0){}
```

단일 표현식인 경우 중괄호를 생략할 수 있다.
```kotlin
fun square(x: Int) = x * x
```

### 함수형 프로그래밍
`stream()` 을 명시하지 않고도 스트림 API 를 사용할 수 있다.  
`it` 이라는 단일 매개변수의 이름을 제공한다.
```kotlin
val doubleList = list.map { it * 2 }
```

> 위 코드에서 소괄호를 생략한 것을 확인할 수 있다.  
> 
> [공식 문서](https://kotlinlang.org/docs/lambdas.html#passing-trailing-lambdas) 에 따르면,  함수의 마지막 매개변수가 함수인 경우,   
> 해당 인수로 전달된 람다 표현식을 괄호 밖에 배치할 수 있고,   
> 람다가 유일한 인수인 경우 괄호를 완전히 생략할 수 있다. (어색하다)
> 
>![image](https://gist.github.com/user-attachments/assets/9d7606b3-1665-49d3-a5fd-bf4ae10a8820)

### 확장 함수
```kotlin
fun List<Int>.lastElement(): Int = this.get(this.size - 1) // 확장 함수 구현
```
---

### `for` 반복문

`int i=1; i<=10; i++` 을 다음과 같이 간략히 작성할 수 있다.

```kotlin
var sum = 0
for (i in 1..10) {
    sum += i
}
println(sum)
```

내림차순은 `downTo` , 건너뜀은 `step` 키워드로 사용할 수 있다.
```kotlin
for(i in 10 downTo 0 step 2) {}
```

### `when` 조건문  
```kotlin
fun foo(f: Int): String {
    val result: String = when(f) {
        1 -> "한 주의 시작"
        2, 3, 4 -> "주중"
        else -> throw IllegalArgumentException("잘못되 날 : $f")
    }
    return result
}
```

인자를 생략하고, 다양한 타입으로 비교할 수도 있다.
```kotlin
var foo2 =  when {
        number in 3..5 -> "숫자"
        char  ==  "a" -> "문자"
}
```

---

### 가시성 제어자
자바에서의 `접근 제어자` 를 코틀린에서는 `가시성 제어자` 라고 부른다.  
- `public` : 자바와 달리 `public` 이 생략시 기본값이다.
- `internal`: 자바에서의 `package-private` 
- `private`
- `protected`

### `;` 사용

라인 끝에 세미콜론을 붙일 필요가 없다.  
줄바꿈으로 라인을 구분하지만, 세미콜론 또한 구문의 끝으로 인식한다.

---

### 클래스
#### **클래스가 필수가 아니다!**