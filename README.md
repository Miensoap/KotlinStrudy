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

### 1. 함수
선언에 `fun` 키워드를 사용한다.  
리턴 타입은 맨 뒤에 선언한다.  
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
```kotlin
fun overloadFun(paramA: Int, paramB: Int, paramC: Int = 0){}
```

###  2. 변수
`var` 키워드로 선언하고, 뒤이어 변수명과 타입을 작성한다.  
타입 추론이 가능해, 선언시 타입을 정하지 않아도 된다.

```java
//자바
int result = square(5);
```
```kotlin
var result: Int = square(5)
```

### 3. `for` 반복문

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

### 4. `when` 조건문  
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

### 클래스
### **클래스가 필수가 아니다!**  

*`println()` 으로 `System.out.println()` 을 호출할 수 있다.*

### `;` 사용

라인 끝에 세미콜론을 붙일 필요가 없다.  
줄바꿈으로 라인을 구분하지만, 세미콜론 또한 구문의 끝으로 인식한다.





