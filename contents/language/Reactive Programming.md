# Reactive Programming

## Reactive Programming(반응형 프로그래밍)이란?
> 데이터 스트림과 변화의 전달(데이터 스트림에서 값이 변했을 때 전달이 이루어지는 것)에 대한 선언적 프로그래밍 패러다임
- 이해하기 위한 문장
   >명령형 프로그래밍에서 a = b + c 를 실행하면 b + c 의 결과가 할당되고,   
    b, c 의 값의 변화는 a에 영향을 주지 않습니다.   
    반면, 리액티브 프로그래밍에서는 b 와 c의 값이 변경될 때마다 a = b + c를 실행하지 않고  
    자동으로 업데이트되어 a의 값을 결정합니다.
    
- 요약하자면 Reactive Programming은 `데이터 스트림`을 `비동기적`인 흐름으로 처리하는 프로그래밍(?)이라고 볼 수 있다.
- 프로그래머가 어떠한 기능을 직접 정해서 실행하는 것이 아닌, `시스템에 이벤트가 발생했을 때` 알아서 처리된다.
- 기존의 프로그래밍 방식을 `Pull 방식`, Reactive Programming 방식을 `Push 방식`이라고도 한다.
    - Pull 방식: 비동기 request를 던지고 response를 기다렸다가 `callback`으로 받아서 처리
    - Push 방식: 비동기 request를 던지고 외부 데이터 스트림에 대한 `subscribe` 형식으로 반응하도록 처리
- Reactive Programming은 `주변 환경과 끊임없이 상호작용`을 하는데, 프로그램이 주도하는 것이 아닌 환경이 변하면 이벤트를 받아 동작함으로써 상호작용한다.
- 다양한 언어에서 비동기 프로그래밍을 위해 `ReactiveX`를 사용한다.

<br>

## ReactiveX(Reactive eXtensions)란?

> Rx라고도 하며, 관찰 가능한(observable) 스트림을 통해 비동기, 이벤트 기반 프로그램을 구성하기 위한 라이브러리(API)
- `Observer 패턴`을 확장하여 `데이터 및 이벤트의 시퀀스`를 지원한다.
- 낮은 수준의 스레딩, 동기화, 스레드 안전성, 동시 데이터 구조 및 non-blocking I/O에 관한 우려를 줄인다.
    - non-blocking: A 함수가 B 함수를 호출할 때, B 함수가 제어권을 바로 A 함수에게 넘겨주면서, A 함수가 다른 일을 할 수 있도록 하는 것

<br>

## Rx의 작동 방식
- Rx에서는 `Observable 객체`를 통해서 `이벤트의 흐름을 표현`한다.
- 그 후, `Operator`를 통해서 Observable이 내뱉는 `이벤트의 값들을 해당 형태로 조합하고 변경`한다.

<img src="./Images/Reactive Programming/Flow.png">

<br>

## Rx의 3요소
### 1. Oberservable
> `관찰할 수 있는` 데이터 스트림
- 보통 Observable은 어떠한 `순차적인 데이터`를 갖게 된다.
- 이 데이터 스트림을 관찰하게 되는 `Observer`들은 `Observer 패턴`을 사용하여 `Observable이 발행하는 데이터에 즉각 반응`할 수 있다.
### 2. Operator
> Observable의 `입력들을 입력받아 결과로 출력`해내는 연산자
- 대부분의 연산자는 `Observable에서 작동`하고 `Observable을 반환`한다.
- 이러한 연산자를 `체인에서 차례로 적용`할 수 있다.
- Rx에서는 생성, 변환, 필터링, 결합, 오류 처리 등 수많은 연산자가 존재한다.
### 3. Schedulers
- Observable 연산자에 멀티스레딩을 도입하려면 해당 연산자 또는 특정 Observable이 특정 스케쥴러에서 작동하도록 지시할 수 있다.

<br>

## Rx의 이벤트 감지
- Observable은 `Emitter`에 포함되어 있는 3가지 이벤트를 활용하여 감시자에게 이벤트를 알릴 수 있다.
- Observable에서 데이터, 오류 등을 발행할 때 `null`은 발행되지 않는다.
- 항상 `onComplete()` 혹은 `onError()` 둘 중 하나로만 데이터 발행이 종료되어야 한다.
### 1. onNext()
> 데이터가 `하나 발행`됐음을 알리는 이벤트
- 연속된 데이터의 경우, 데이터가 하나씩 차례대로 `onNext()`로 발행된다.
### 2. onComplete()
> 데이터 발행이 `모두 완료`되었음을 알리는 이벤트
- `onComplete()`가 호출된 이후에는 더이상 `onNext()`가 호출이 되지 않는다.
### 3. onError()
> `오류가 발생`했음을 알리는 이벤트
- 마찬가지로 `onError()`가 호출된 이후에는 더이상 `onNext()`가 호출이 되지 않는다.

<br>

## Rx의 장점
### 1. 이벤트 스트림 또는 데이터 스트림을 쉽게 생성할 수 있다.
### 2. 쿼리와 같은 연산자로 스트림을 작성하고 변환한다.
### 3. Side effect를 일으킬수 있는 관찰 가능한 모든 스트림을 구독할 수 있다.
### 4. 코드 관련 장점
- Functional   
  관측 가능한 스트림을 통해 깔끔하게 입/출력 함수를 사용하여 복잡한 프로그램을 피할 수 있다.
- Less is more   
  정교하고 복잡한 문제를 몇 줄의 코드로 줄일수 있다.
- Async error handling   
  전통적인 try/catch는 비동기 에러는 처리할 수 없지만 Rx는 비동기 에러도 처리할 수 있다.
- Concurrency amd easy   
  낮은 수준의 스레딩, 동기화 및 동시성 문제를 간단하게 추상화 할 수 있다.

<br>

## Rx의 단점
### 1. 러닝커브가 높아 학습이 어렵다.
### 2. 디버깅이 어렵다.

<br>

## RxSwift 예시
```Swift
// 기존 코드
Network.download(file: "https://www...")
    .subscribe(onNext: { data insequence
    	// 데이터 추가
    },
    onError: { error in
    	// 에러 표현
    },
    onCompleted: {
    	// 다운로드 된 파일 사용
    })
```
- Network.download가 Observable
- onNext() 이벤트를 통해 데이터를 받고, onError() 이벤트를 통해 에러가 발생하면 에러를 표현한다. onComplete() 이벤트를 받으면 액션을 취할 수 있다.

```Swift
UIDevice.rx.orientation
    .filter { value in
    	return value != .landscape
    }
    .map { _ in
    	return "세로모드"
    }
    .subscribe(onNext: { string in
    	showAlert(text: string)
    })
```
- fileter 연산자를 사용해 orientation이 세로인 경우에만 필더링한다.
- 가로인 경우에는 이벤트가 아예 생성되지 않는다.
- map 연산자를 사용해 string 출력으로 변환되고 마지막으로 subscribe()를 통해 onNext() 이벤트를 구독한다.

<br>

## ReactiveX를 지원하는 언어들
- Java: RxJava
- JavaScript: RxJS
- C#: Rx.NET
- C#(Unity): UniRx
- Scala: RxScala
- Clojure: RxClojure
- C++: RxCpp
- Lua: RxLua
- Ruby: Rx.rb
- Python: RxPY
- Go: RxGo
- Groovy: RxGroovy
- JRuby: RxJRuby
- Kotlin: RxKotlin
- Swift: RxSwift
- PHP: RxPHP
- Elixir: reaxive
- Dart: RxDart

<br>

---
### Reference

<a href="https://4z7l.github.io/2020/12/01/rxjava-1.html">[RxJava] RxJava 이해하기 - 1. Reactive Programming 이란</a>

<a href="https://reactivex.io/intro.html">ReactiveX</a>

<a href="https://velog.io/@haero_kim/Reactive-X-Observable-%EA%B0%9C%EB%85%90-%EB%82%A0%EB%A8%B9%ED%95%98%EA%B8%B0">[Reactive X] Observable 개념 날먹하기</a>
