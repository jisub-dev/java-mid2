# Section 1. 제네릭 - Generic1
* 코드 재사용과 타입 안정성을 동시에 잡기 -> Object를 사용하면 코드 재상용성을 올라감, 하지만 무모한 다운 캐스팅을 하기 때문에 타입 안정성이 떨어짐
* <T> : 다이아몬드라고 읽음. T를 타입 매개변수라고 한다. 이후에 Integer, String 같은 객체 참조 타입으로 바뀔 수 있다(int 와 같은 기본형은 안됨)
* 제네릭 생성시 타입을 생략하여 알아서 추론할 수 있게 할 수 있다. 타입 추론은 자바 컴파일러가 타입을 추론할 수 있는 상황에서만 가능하다
```java
GenericBox<Integer> integerBox2 = new GenericBox<>();
```
* 제네릭은 코드 재사용, 타입 안정성 모두 잡을 수 있다
* 매개변수는 메서드를 선언할 때 사용하는 것이고, 인자(인수)는 작동할 떄 값을 넘기는 그 값을 인자라고 한다
* 메서드: 매개변수에 인자를 전달해서 사용할 값을 결정
* 제네릭 클래스(제네릭 타입): 타입 매개변수에 타입 인자를 전달해서 사용할 값을 결정
* GenericBox<Integer> integerBox = new GenericBox<Integer>(); 에서 new GenericBox<Integer>() 의 Integer 가 타입 인자이다
* 타입 인자: 제네릭 타입을 사용할 때 제공되는 실제 타입
* public class GenericBox<T> 에서 T가 타입 매개변수이다
* 보통 제네릭은 용도에 맞는 단어의 첫 글자를 사용하는 관례를 따른다. Ex) E - Element, T - Type 등
* 아래와 같이 제네릭 타입을 명시하지 않는 경우가 있는데, 이런것을 raw type, 원시 타입이라고 한다 (이는 옛날 자바 코드와 호환하기 시키기 위해 남겨둔 것이다. 하지만 지금 버전에서는 사용하면 안됨)
```java
        GenericBox integerBox = new GenericBox();
```

