# JSON VS XML

## JSON이란?

> JavaScript Object Notation의 약자로, 데이터를 조금 더 쉽게 교환하고 저장하기 위해 만들어진 텍스트 기반의 데이터 교환 표준

- 데이터가 `속성-값` 또는 `키-값` 쌍으로 이루어져있다. 
- `자바 스크립트를 기반`으로 만들어졌다.
- `XML의 대안`으로, 조금 더 쉽게 데이터를 교환하고 저장하기 위해 고안되었다.
- `텍스트 기반`이므로, `어떠한 프로그래밍 언어에서도 JSON 데이터를 읽고 사용`할 수 있다.

<br>

### JSON의 특징

- 사용하기 쉽다.
- 적은 메모리 공간을 사용하기 때문에 빠르다.
- 자바스크립트를 확장하여 만들어졌다.
- 자바스크립트 객체 표기법을 따른다.
- 사람과 기계가 모두 읽기 편하도록 고안되었다.
- 프로그래밍 언어와 운영체제에 독립적이다.

<br>

### JSON의 장점

- 모든 브라우저에 대한 지원을 제공한다.
- 생성, 조작, 읽기, 쓰기가 쉽다.
- 구문이 간단하다.
- 직렬화가 가능하다.

<br>

### JSON의 단점

- 네임 스페이스 지원이 없다.   
(확장성이 부족하다.)
- 문법을 지켜야 한다.
- 제한된 개발 도구를 지원한다.

<br>

---

## XML이란?

> EXtensible Markup Language의 약자로, 데이터를 저장하고 전달할 목적으로 만들어졌으며, 저장되는 데이터의 구조를 기술하기 위한 언어

- `<` 로 시작하여 `>` 로 끝나는 마크업 구조이다.
- 수많은 응용 분야에서 데이터를 저장하고 전달하는 중요한 역할을 맡고 있다.
- XML을 배우기 전에 HTML, 자바스크립트 등의 기초 지식이 필요하다.

<br>

### XML의 특징

- 다른 목적의 마크업 언어를 만드는 데 사용되는 `다목적 마크업 언어`이다.
- 다른 시스템끼리 `다양한 종류의 데이터를 손쉽게 교환`할 수 있도록 해준다.
- 새로운 태그를 만들어 추가해도 계속해서 동작하므로, `확장성`이 좋다.
- 데이터를 보여주지 않고, `데이터를 전달하고 저장하는 것만을 목적`으로 한다.
- `텍스트 데이터 형식`의 언어로, 모든 XML 문서는 `유니코드` 문자로만 이루어진다.

<br>

### XML의 장점

- 시스템 및 애플리케이션 간에 문서 전송이 가능하다.
- 플랫폼이 독립적이기 때문에 서로 다른 플랫폼 간에 데이터 교환이 가능하다.

<br>

### XML의 단점

- 처리 응용 프로그램이 필요하다.
- XML 구문이 중복된다.

<br>

---

## JSON과 XML의 공통점

- 데이터를 저장하고 전달하기 위해 고안되었다.
- 기계뿐만 아니라 사람도 쉽게 읽을 수 있다.
- 계층적인 데이터 구조를 가진다.
- 다양한 프로그래밍 언어에 의해 파싱될 수 있다.

<br>

## JSON과 XML의 차이점

- JSON은 종료 태그를 사용하지 않는다.
- JSON의 구문이 XML의 구문보다 더 짧다.
- JSON 데이터가 XML 데이터보다 더 빨리 읽고 쓸 수 있다.
- XML은 배열을 사용할 수 없지만, JSON은 배열을 사용할 수 있다.
- XML은 XML 파서로 파싱되며, JSON은 자바스크립트 표준 함수인 eval() 함수로 파싱된다.
- XML 문서는 XML DOM(Document Object Model)을 이용하여 해당 문서에 접근하지만, JSON은 문자열을 전송받은 후에 해당 문자열을 바로 파싱하므로, XML보다 더욱 빠른 처리 속도를 보여준다.
- JSON은 전송 받은 데이터의 무결성을 사용자가 직접 검증해야 하지만, XML은 데이터의 검증이 필요한 곳에서 스키마를 사용하여 데이터의 무결성을 검증할 수 있다.
- JSON은 네임스페이스를 지원하지 않고, XML은 네임스페이스를 지원한다.   

<br>

### 예시

- JSON 예시
```JSON
{
    "study": [
        { "name": "Kim", "age": 22 },
        { "name": "Kim", "age": 24 },
        { "name": "Ji", "age": 24 },
        { "name": "Kwon", "age": 24 },
        { "name": "Lee", "age": 25 }
    ]
}
```

- XML 예시
```XML
<study>
    <info>
        <name>Kim</name> <age>22</age>
    </info>
    <info>
        <name>Kim</name> <age>24</age>
    </info>
    <info>
        <name>Ji</name> <age>24</age>
    </info>
    <info>
        <name>Kwon</name> <age>24</age>
    </info>
    <info>
        <name>Lee</name> <age>25</age>
    </info>
</study>
```
- XML 네임스페이스
```XML
<root

    xmlns:a="https://www.w3.org/TR/html5/"

    xmlns:b="http://codingsam.com/xml/physical/">

    <a:body>

        <a:h1>html에서의 제목</a:h1>

        <a:p>html에서의 단락</a:p>

    </a:body>

    <b:body>

        <b:arm>70</b:arm>

        <b:leg>110</b:leg>

    </b:body>

</root>
```
<br>

---

### Reference

<a href="https://velog.io/@cil05265/XML%EA%B3%BC-JSON%EC%9D%98-%ED%8A%B9%EC%A7%95-%EA%B3%B5%ED%86%B5%EC%A0%90-%EC%B0%A8%EC%9D%B4%EC%A0%90">XML과 JSON의 특징, 공통점, 차이점</a>

<a href="https://sujl95.tistory.com/59">Json과 XML의 차이</a>

<a href="http://www.tcpschool.com/xml/xml_basic_namespace">XML 네임스페이스</a>