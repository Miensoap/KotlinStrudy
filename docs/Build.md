## 코틀린 코드는 어떻게 빌드될까?

코틀린은 자바와 마찬가지로 `JVM` 에서 실행되기 때문에, `바이트 코드` 로 변환된다.

`Hello.kt` 파일을 컴파일하면, `HelloKt.class` 파일이 생성된다.  

`JRE`  에는 `JVM` 뿐만 아니라, 자바 코드에서 사용할 수 있는각종 라이브러리가 포함되는데,  
코틀린은 이를 사용하기 위해,  컴파일시 기본 클래스를 함께 묶어 `jar` 로 배포하는 방식을 사용한다.  

> `kotlinc Array.kt -include-runtime -d array.jar`  

위와 같이 `include-runtime` 옵션을 부여해 컴파일하면,   
필요한 클래스 파일들과 메타데이터, 리소스를 모두 포함한 `jar` 라는 패키지 파일이 생성된다.

이후로는 자바 코드를 `jar` 로 빌드한 것과 동일하게 실행 가능하다.


> 바이트 코드로 실행되기 때문에 당연히 실행 시간은 자바와 동일하지만,  
`kotlic` 를 사용하는 컴파일은 `javac` 보다 느리다.  (2023.09.20 출판 서적 참고)    
> 
>2024년 5월 [`K2 컴파일러`](https://blog.jetbrains.com/ko/kotlin/2024/05/celebrating-kotlin-2-0-fast-smart-and-multiplatform/) 가 출시되었는데, 컴파일링 속도를 개선했다고 한다.