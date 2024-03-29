# 부록 C 동적인 협력, 정적인 코드

- 동적 모델
    - 프로그램의 실행 구조를 표현하는 움직이는 모델
- 정적 모델
    - 코드의 구조를 담는 고정된 모델
- 정적 모델은 동적 모델에 의해 주도돼야 하며 동적 모델이라는 토대 위에 세워져야 한다.
- 정적 모델은 객체 사이의 협력에 기반해야 한다.

## 동적모델과 정적 모델

### 행동이 코드를 결정한다

- 행동이 객체의 정적 모델을 결정해야 한다.
- 가장 중요한 것은 객체가 외부에 제공하는 행동이다.

### 변경을 고려하라

- 동일한 행동을 제공하는 정적 모델이 있다면 항상 현재의 설계에서 요구되는 변경을 부드럽게 수용할 수 있는 설계를 선택하라.

## 도메인 모델과 구현

### 도메인 모델에 관하여

- 도메인
    - 프로그램을 사용하는 대상 영역
- 모델
    - 지식을 선택적으로 단순화하고 의식적으로 구조화한 형태
- 도메인 모델
    - 대상 영역에 대한 지식을 선택적으로 단순화하고 의식적으로 구조화한 형태
    - 도메인 모델을 작성하는 것이 목표가 아니라 출발점
    - 도메인 모델의 역할은 필요한 개념의 이름과 의미 그리고 관계에 대한 힌트를 제공하는 것이다.
- 도메인 모델에 지나치게 집착해서는 안된다.
    - **중요햔 것은 소프트웨어의 기능, 객체의 책임 그리고 개체의 협력이다.**

### 몬스터 설계하기

- 새로운 클래스를 추가하지 않고도 새로운 기능을 추가할 수 있는 방법
    - 합성을 이용하면 된다.
    - ex) 새로운 몬스터를 추가하자
        - 상속을 사용하지 않고 클래스 내에 몬스터의 종류를 표현하는 크래스를 포함시킨다.
- TYPE OBJECT 패턴
    - 인스턴스가 다른 인스턴스의 타입을 표현하는 방법

### 행동과 변경을 고려한 도메인 모델

- 객체지향의 핵심은 객체 사이의 협력
- 도메인의 핵심을 간략하게 단순화해서 표현할 수 있는 모든 것이 도메인 모델이다.
- 도메인 모델에는 객체의 행동과 변경에 기반해야 하며 코드의 구조를 반영해야 한다.

### 분석 모델, 설계 모델 그리고 구현 모델

- `분석 모델`
    - 순수하게 문제 도메인에 초점
- `설계 모델`
    - 기술적인 관점에서 솔루션을 서술
- `구현 모델`
    - 프로그래밍 언어를 사용해 컴퓨터가 이해할 수 있는 명령어로 변환
- 위의 3가지 모델은 모두 행동과 변경이라는 요소에 영향을 받으며 전체 개발 주기 동안 동일한 모야을 지녀야 한다.
