## 1.1 역사의 흐름은 무엇인가?
자바 역사를 통들어 가장 큰 변화가 일어난 버전은 8버전이다.
이 버전을 이용하면 자연어에 더 가깝게 간단한 방식으로 코드를 구현할 수 있다.

사과의 무게를 비교 후 정렬하는 고전 코드
``` java
Collections.sort(inventory, new Comparator<Apple>() {
	public int compare(Apple a1, Apple a2) {
		return a1.getWeight().compareTo(a2.getWeight());
	}
});
```
자바 8
``` java
inventory.sort(comparing(Apple::getWeight))
```

자바 8에서는 병렬 실행 환경이 쉽게 관리될 수 있고 에러가 덜 발생하는 방법을 제공한다.

자바 8에서 제공하는 새로운 기술
- 스트림 API (병렬 연산을 지원!, Synchronized를 사용하지 않아도 됨!)
- 메서드에 코드를 전달하는 기법(메서드 참조와 람다)
- 인터페이스의 디폴트 메소드

## 1.2 왜 아직도 자바는 변화하는가?
새로운 언어가 등장하면서 진화하지 않는 기존 언어는 사장되었다.
모든 언어가 장단점을 갖고 있고 완벽한 언어는 없다.

### 1.2.1 프로그래밍 언어 생태계에서 자바의 위치
코드를 JVM를 통해 바이트 코드로 컴파일하는 특징때문에 자바는 웹 프로그램의 주요 언어가 되었다. 이게 가능했던 이유는 모든 브라우저가 가상 머신 코드를 지원하였기 때문이다. (이 점을 노린 듯)

- 어떻게 대중적인 프로그래밍 언어로 성장했는가?
`캡슐화`, `객체지향의 정신적인 모델`?, `일단 말들면 모든 곳에서 실행할 수 있었다`

빅데이터를 직면하며 병렬 프로세싱을 활옹해야 하는데 지금까지의 자바로는 충분히 대응할 수 없었다.

자바 8의 새로운 멀티코어 병렬성이 강화된 이유를 설명할 예정이다.

### 1.2.2 스트림 처리
`스트림 처리`
> 스트림이란 한 번에 한 개씩 만들어지는 연속적인 데이터 항목들의 모임이다.
> 어떤 프로그램의 출력 스트림은 다른 프로그램의 입력 스트림이 될 수 있다.

자바 8에는 java.util.stream 패키지에 Stream API가 추가되었다.
스트림 패키지에 정의된 Stream<T>는 T형식으로 구성된 일련의 항목을 의미힌다.
스트림 API의 핵심은 기존에는 한 번에 한 항목을 처리했지만 고수준으로 추상화해서 일련의 스트림으로 만들어 처리할 수 있다는 것이다.
스레드라는 복잡한 작업을 하지 않고도 병렬성을 얻을 수 있다는 것이다.

### 1.2.3 동작 파라미터화로 메서드에 코드 전달하기
`동작 파라미터화(Behavior prameterization)`란?
> 코드 일부를 API로 전달하는 기능
> 메서드를 다른 메서드의 인수로 넘겨주는 기능을 제공한다.

스트림 API는 연산의 동작을 파라미터화할 수 있는 코드를 전달한다는 사상에 기초한다.

compareUsingCustomerId 메서드를 sort의 인수로 전달
``` java
public int compareUsingCustomerId(Sring inv1, String inv2) {
    // ....
}
```

### 1.2.4 병렬성과 공유 가변 데이터
`병렬성을 공짜로 얻을 수 있다`

`순수(pure) 함수` `부작용 없는(side-effect-free) 함수` `상태 없는 (Stateless) 함수`란?
**안전하게 실행**할 수 있는 코드를 만들려면 공유된 가변 데이터에 접근하지 않아야한다.

`함수형 프로그래밍` 패러다임의 핵심적인 사항
- 공유되지 않은 가변 데이터
- 메서드
- 함수 코드를 다른 메서드로 전달하는 기능

`명령형 프로그래밍` 패러다임
- 일련의 가변 상태로 프로그램을 정의

### 1.2.5 자바가 진화해야 하는 이유
자바의 변화에 따라 편리함이 증가한다.
예를 들면 이런 코드
```java
List<String> list = new ArrayList<>();
```

## 1.3 자바 함수
- 프로그래밍 언어에서 `함수` 용어는 특히 `정적 메서드`와 같은 의미로 사용된다.
- 프로그래밍 언어의 핵심은 `값`을 바꾸는 것이다. 이 값을 일급값 또는 시민이라고 부른다.
- 메서드, 클래스 등은 `이급 시민`
  
### 1.3.1 메서드와 람다를 일급 시민으로
- 메소드를 일급값으로 사용하여 프로그래밍이 수월해진다는 강력한 기능떄문에 일급 시민이 부족한 다른 프로그래밍언어를 기피하는 현상까지 발생한다.
- 자바 8에서는 일급값을 제공하기 위해 기능을 설계하였다.
	- `매서드 참조(method reference)`
	``` java
	// 자바 8 이전 코드
	File[] hiddenFiles = new File(".").listFiles(new FileFilter() {
		public boolean accept(File file) {
			return file.isHidden();
		}
	});
	// 자바 8
	File[] hiddenFiles = new File(".").listFile(File::isHidden);
	```
	- 위와 같은 자바 8 코드가 있을 때, `::`는 'File의 isHidden 값으로 사용하라'는 의미이다.
	- isHidden은 이미 준비되어 있는 `함수`이다.
	- `람다 : 익명 함수`
		- 자바 8 에서는 기명 메서드를 일급값으로 취급할 뿐 아니라
		**람다**(또는 익명 함수)를 포함하여 함수도 값으로 취급할 수 있다.
		- (int x) -> x + 1

### 1.3.2 코드 넘겨주기 : 예제
- 예제 코드 : `http://www.hanbit.co.kr/src/10202`
- `필터 ` : 특정 항목을 선택해서 반환하는 동작 (ex. 사과들 중 녹색사과만 선택해서 리스트를 반환하는 프로그램)
``` java
public static boolean isGreenApple(Apple apple) {
    return GREEN.equals(apple.getColor());
}

public static boolean isHeavyApple(Apple apple) {
    return apple.getWeight() > 150;
}

public interface Predicate<T>{
    boolean test(T t);
}

static List<Apple> filterApples(List<Apple> inventory, Predicate<Apple> p) {
    List<Apple> result = new ArrayList<>();
    for (Apple apple : inventory) {
        if(p.test(apple)) {
            result.add(apple);
        }
    }
    return result;
}

filterApples(inventory, Apple::isGreenApple)
filterApples(inventory, Apple::isHeavyApple)
```

### 1.3.3 메서드 전달에서 람다로
매번 사용할 메서드를 정의하는 것은 번거롭다.
람다를 활용해서 쉽게 구현이 가능하다.
``` java
filterApples(inventory, (Apple a) -> GREEN.equals(a.getColor()));
```

## 1.4 스트림

`스트림`
스트림 API 이전 컬렉션 API를 이용하여 다양한 로직을 처리하였을 것이다. 
스트림 API를 이용하면 컬렉션 API와는 상당히 다른 방식으로 데이터를 처리할 수 있다. 
컬렉션 API를 사용하 for-each 루프를 이용하여 각 요소를 반복하면서 작업을 수행했다. 
이러한 방식의 반복을 **외부 반복(external iteration)** 이라 한다. 
반면 스트림 API를 이용하면 루프를 신경 쓸 필요가 없다. 
스트림 API에서는 라이브러리 내부에서 모든 데이터가 처리된다. 이와 같은 반복을 **내부 반복(internal iteration)** 이라고 한다.
``` java
  // 자바 8 이전 
  private static void groupImperatively() {
    Map<Currency, List<Transaction>> transactionsByCurrencies = new HashMap<>();
    for (Transaction transaction : transactions) {
      Currency currency = transaction.getCurrency();
      List<Transaction> transactionsForCurrency = transactionsByCurrencies.get(currency);
      if (transactionsForCurrency == null) {
        transactionsForCurrency = new ArrayList<>();
        transactionsByCurrencies.put(currency, transactionsForCurrency);
      }
      transactionsForCurrency.add(transaction);
    }
  }
  
  // 자바 8
  private static void groupFunctionally() {
    Map<Currency, List<Transaction>> transactionsByCurrencies = transactions.stream()
        .collect(groupingBy(Transaction::getCurrency));
  }
```

### 1.4.1 멀티 스레딩은 어렵다
Java 8 버전 이전의 경우에는 기존 스레드 API로 멀티스레딩 코드를 구현해서 병렬성을 이용하는 것은 쉽지 않다. (스레드를 직접 제어해야함)
자바 스트림 API는 `컬렉션을 처리하면서 발생하는 모호함과 반복적인 코드 문제` 그리고 `멀티코어 활용 어려움`이라는 문제를 해결했다.
내부적으로 포크 조인(Fork-Join)방식을 사용한다.

## 1.5 디폴트 메서드와 자바 모듈
기존 자바 기능으로는 대규모 컴포넌트 기반 프로그래밍 그리고 진화하는 시스템의 인터페이스를 적절히 대응하기 어려웠다. 자바 8에서 지원하는 디폴트 메서드를 이용해 기존 인터페이스를 구현하는 클래스를 바꾸지 않고도 인터페이스를 변경할 수 있다.

예를 들어 List/나 Collection/ 인터페이스는 이전에 stream이나 parallelStream 메서드를 지원하지 않았다. 하지만 자바 8에서 Collection 인터페이스에 stream메서드를 추가하고 이를 디폴트 메서드로 제공하여 기존 인터페이스를 쉽게 변경할 수 있었다.

## 1.6 함수형 프로그래밍에서 가져온 다른 유용한 아이디어
자바 8에서는 NPE(NullPointerException)을 피할 수 있도록 도와주는 Optional<T> 클래스를 제공한다.