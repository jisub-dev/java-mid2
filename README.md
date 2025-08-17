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
* 만약 제네릭 타입과 맟지 않는 데이터를 넣을 시 컴파일 오류가 발생한다

# Section 2. 제네릭 - Generic2
* 제레릭 타입도 원하는 타입만 들어올 수 있게 제한하고 싶을 때가 있다. 이럴때 public class AnimalHospitalV4<T extends Animal> 이런식으로 `제네릭타입 extends 원하는타입(자식포함)` 처럼 사용할 수 있다
* 이는 기존에 모든 타입이 들어왔었지만 Animal 을 상한으로 두어 Animal과 그 기능들을 사용할 수 있게 되었다
* 제네릭 메서드와 제네릭 타입은 완전히 다르다
  * 제네릭 메서드는 메서드 스코프이지만
  * 제네릭 타입은 클래스 스코프이다
* Number : int, double의 부모
* 제네릭 타입
  * 정의: GenericClass<T>
  * 예) new GenericClass<String>
* 제네릭 메서드
  * 정의: <T> T genericMethod(T t)
  * 타입 인자 전달: 메서드를 호출하는 시점
  * 예) GenericMethod.<Integer>genericMethod(i)
* 제네릭 메서드는 static 메서드에 도입 가능하고, 인스턴스 메서드에도 도입이 가능하다
* 제네릭 타입은 static 메서드에 타입 매개변수를 사용할 수 없다. 왜냐하면 제네릭 타입은 객체를 생성하는 시점에 타입이 정해지는데 static 메서드는 인스턴스 단위가 아니라 클래스 단위이기 때문에 제네릭 타입과는 무관하다.
* 만약 static 메서드에 제네릭을 도입하려면 제네릭 메서드를 사용해야 한다
* 타입 추론 기능 덕분에 명시적으로 타입을 지정하지 않아도 된다
```java
        Integer result = GenericMethod.<Integer>genericMethod(i); // 명시적 지정 시
        Integer result2 = GenericMethod.genericMethod(i); // 추론 시
```
* 아래와 같이 다른 타입의 인자가 들어온다면 컴파일 오류가 발생한다. 메서드의 T가 하나의 타입으로 결정되기 때문이다
```java
public static <T extends Animal> T getBigger(T t1, T t2) {
        return t1.getSize() > t2.getSize() ? t1 : t2;
    }
```
* 정적 메서드는 제네릭 메서드만 적용가능
* 인스턴스 메서드는 제네릭 타입과 제네릭 메서드 둘 다 적용 가능
* 우선순위
  * 제네릭 메서드 > 제네릭 타입
* 아래 코드에서 printAndReturn(Z z)는 제네릭 메서드로 제네릭 타입인 T와 구분된다
  * 제네릭 타입인 T는 상한이 Animal이지만 제네릭 메서드 Z는 상한이 Object이다
  * 또한 제네릭 타입과 제네릭 메서드를 T와 같이 같은 이름으로 두면 모호해지므로 T, Z와 같이 구분할 수 있게 해줘야 한다
```java
package generic.ex4;

import generic.animal.Animal;

public class ComplexBox<T extends Animal> {

    private T animal;

    public void set(T animal) {
        this.animal = animal;
    }

  public <Z> Z printAndReturn(Z z) {
      System.out.println("animal.className: " + animal.getClass().getName());
      System.out.println("t.className: " + z.getClass().getName());
      return z;
  }
}

```
* 제네릭 메서드의 상한은 아래와 같이 설정할 수 있다
```java
public <Z extends Number> Z printAndReturn(Z z) {
    System.out.println("animal.className: " + animal.getClass().getName());
    System.out.println("z.className: " + z.getClass().getName());
    return z;
}
```
* <?>인 와일드 카드를 사용하면 제네릭 메서드가 아니라 일반적인 메서드이다
* <?>을 사용하면 모든 타입을 받을 수 있다 (Object로 반환 됨)
* 제네릭 메서드 작동 원리
  1. 호출
  2. 제네릭 타입 결정
  3. 타입 인자 결정
  4. 최종 실행
* 제네릭 메서드와 와일드 카드
  * 보통 제네릭 메서드는 타입을 결정해야하므로 더 복잡하다
  * 보통 꼭 필요한 상황이 아니라면 와일드 카드 사용을 권장한다
* <? extends 상한타입> 을 사용하면 상한타입을 포함한 하위 타입만 입력받는다. 그렇지 않으면 컴파일 오류가 발생한다
* 와일드타입을 사용하면 명확하게 타입을 반환할 수 없다
* 메서드의 타입들을 특정 시점에 변경 할 떄 -> 제네릭 타입, 제네릭 메서드 사용
* 이미 만들어진 제네릭 타입을 전달 받아서 활용 할 때 -> 와일드 카드
* 제네릭 타입, 제네릭 메서드를 사용해야하는 상황이 아니면 와일드 카드 사용을 권장한다
* <? super 하한타입> 을 사용하면 하한타입의 상위 타입들만 입력받을 수 있다
* 제네릭은 컴파일 할 때만 사용한다. 컴파일이 끝나면 자바는 제네릭과 관련된 정보를 삭제하고 .java가 .class로 변경된다
* 상한을 설정했을 때 컴파일 시 T가 Animal 타입으로 대체되는 것이다
* 타입 이레이저: 자바의 제네릭 타입은 컴파일 시점에만 존재하고 런타임 시에는 제네릭 정보를 지우는 것
* 아래와 같은 코드에서 T를 Dog로 전달해서 new Dog() 객체를 반환하지 못한다. 컴파일 시점 이후에는 T는 Object 로 대체되기 때문이다
```java
package generic.ex5;

public class EraserBox<T> {
    
    public boolean instanceCheck(Object param) {
        //return param instanceof T;
        return false;
    }
    
    public void create() {
        //return new T(); //오류
    }
}
```
* Shuttle<Marine> shuttle1 = new Shuttle<>(); 이런식으로 새로운 객체를 만들면 제네릭 타입 사용
* shuttle1.in(new Marine("마린", 40)); 이런식으로 메서드 안에 new ~ 가 들어가면 제네릭 타입을 사용하는 클래스에 private T t; 를 만들어서 this.t로 객체 생성
* 