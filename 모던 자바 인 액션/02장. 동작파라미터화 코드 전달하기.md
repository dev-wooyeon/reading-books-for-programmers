시시각각 변하는 사용자 요구사항에 대응하는 방법에 대한 고민
새로 추가하는 기능은 쉽게 할 수 있어야 하고 장기적으로 유지보수가 쉬워야한다.
자주 바뀌는 요구사항에 효과적으로 대응할 수 있도록 **`동작 파라미터화`**를 이용

동작 파리미터화를 추가하려면 쓸데 없는 코드가 늘어난다 Java 8버전에서 이 문제를 해결하기 위해 람다 표현식을 만들었다.
``` java
Comparator<Apple> byWeight = new Comparator<>() {
    public int compare(Apple a1, Apple a2) {
        return a1.getWeight().compareTo(a2.getWeight());
    }
}

// 람다를 이용한 Java 8
Comparator<Apple> byWeight = (Apple a1, Apple a2) -> a1.getWeight().compareTo(a2.getWeight());
```

## 2.2 동작 파라미터화
`Predicate` : 참 또는 거짓을 반환하는 함수

동작 파라미터화 방법
코드 전달 기법을 이용하면 동작을 메서드의 인수로 전달할 수 있다. 하지만 자바 8 이전에는 코드를 지저분하게 구현해야 했다. 익명 클래스로도 어느 정도 코드를 깔끔하게 만들 수 있지만 자바 8에서는 인터페이스를 상속받아 여러 클래스를 구현해야 하는 수고를 없앨 수 있는 방법을 제공한다.

- 선택 조건을 결정하는 (전략)인터페이스 선언(Predicate)

```java
public interface ApplePredicate {
	boolean test(Apple apple);
}
```

- 클래스를 통한 동작 파라미터화

```java
public class AppleGreenColorPredicate implements ApplePerdicate {
	public boolean test(Apple apple) {
		return GREEN.equals(apple.getColor());
	}
}

List<Apple> greenApples = filterApples(inventory, new AppleGreenColorPredicate());
```

- 익명 클래스를 통한 동작 파라미터화

```java
List<Apple> greenApples = filterApples(inventory, new AppleGreenColorPredicate() {
		public boolean test(Apple apple) {
			return GREEN.equals(apple.getColor());
		}
});
```

- 람다를 통한 동작 파라미터화

```java
List<Apple> greenApples
	 = filterApples(inventory, (Apple apple) -> GREEN.equals(apple.getColor()));
```

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FZp1m8%2FbtqP4ltjmFM%2FKzQ26f1to0vP6AI5Kefml0%2Fimg.png)

자바 API의 많은 메서드는 정렬, 스레드, GUI 처리 등을 포함한 다양한 동작으로 파라미터화 할 수 있다.

```java
// ex) java.util.Comparator
public interface Comparator<T> {
	int compare(T o1, T o2)l
}
```

```java
// anonymous class
inventory.sort(new Comparator<Apple>() {
	public int compare(Apple a1, Apple a2) {
		return a1.getWeight().compareTo(a2.getWeight());
	}
});

// lamda
inventory.sort(
	(Apple a1, Apple a2) -> a1.getWeight().compareTo(a2.getWeight()));
```