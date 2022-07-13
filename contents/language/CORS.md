# CORS

`Cross-Origin Resource Sharing, CORS`

다른 출처의 자원을 공유할 수 있도록 설정하는 권한 체제

브라우저에서는 보안적인 이유로 cross-origin HTTP 요청들을 제한한다. 따라서 cross-origin 요청을 하려면 서버의 동의가 필요하다. 만약 서버가 동의한다면 브라우저에서는 요청을 허락하고, 동의하지 않는다면 브라우저에서 거절한다.

그래서 브라우저에서 cross-origin 요청을 안전하게 할 수 있도록 하는 메커니즘이다.

따라서 CORS를 설정해주지 않은 경우, 원하는대로 리소스를 공유하지 못하게 된다.

### `cross-origin` 이란

다음 중 한 가지라도 다른 경우를 말한다.

1. 프로토콜 - http와 https는 프로토콜이 다르다.
2. 도메인 - domain.com과 [other-domain.com](http://other-domain.com) 은 다르다.
3. 포트 번호 - 8080포트와 3000포트는 다르다.

### CORS는 왜 필요한가?

CORS가 없이 모든 곳에서 데이터를 요청할 수 있게 되면, 다른 사이트에서 원래 사이트를 흉내낼 수 있게 된다.

e.g. 기존 사이트와 완전히 동일하게 동작하도록 하여 사용자가 로그인하게 만들고, 로그인하면 세션을 탈취하여 악의적으로 정보를 추출하거나 다른 사람의 정보를 입력하는 등 공격할 수 있다.

따라서 이렇게 공격을 할 수 없도록 브라우저에서 보호하고, 필요한 경우에만 서버와 협의하여 요청할 수 있도록 하기 위해 필요하다.

### CORS는 어떻게 동작하는가?

`Simple requests`인 경우

1. 서버로 요청을 한다.
2. 서버의 응답이 왔을 때 브라우저가 요청한 Orgin 과 헤더 Access-Control-Request-Headers 의 값을 비교하여 유효한 요청이라면 리소스를 응답한다. 만약 유효하지 않은 요청이라면 브라우저에서 이를 막고 에러가 발생한다.

`Simple request`란?

HTTP method가 다음 중 하나이면서

- GET
- HEAD
- POST

자동으로 설정되는 헤더는 제외하고, 설정할 수 있는 다음 헤더들만 변경하면서

- Accept
- Accept-Language
- Content-Language

`Content-Type`이 다음과 같은 경우

- application/x-www-form-urlencoded
- multipart/form-data
- text/plain

Simple request라고 부른다. 이 요청은 추가적으로 확인하지 않고 바로 본 요청을 보낸다.

### preflight 요청일 경우

1. Origin 헤더에 `현재 요청하는 origin`과, `Access-Control-Request-Method` 헤더에 요청하는 HTTP method와 `Access-Control-Request-Headers` 요청 시 사용할 헤더를 `OPTIONS` 메서드로 서버로 요청한다. 이때 내용물은 없이 헤더만 전송한다.
2. 브라우저가 서버에서 응답한 헤더를 보고 유효한 요청인지 확인한다. 만약 유효하지 않은 요청이라면 요청은 중단되고 에러가 발생한다. 만약 유효한 요청이라면 원래 요청으로 보내려던 요청을 다시 요청하여 리소스를 응답받는다.

### preflight 요청이란?

Simple requests가 아닌 cross-origin 요청은 모두 preflight 요청을 하게 되는데, 실제 요청을 보내는 것이 안전한지 확인하기 위해 먼저 OPTIONS 메서드를 사용하여 cross-origin HTTP 요청을 보낸다. 이렇게 하는 이유는 사용자 데이터에 영향을 미칠 수 있는 요청이므로 사전에 확인 후 본 요청을 보낸다.

### 요청 헤더 목록

- Origin
- Access-Control-Request-Method
    - `preflight` 요청을 할 때 실제 요청에서 어떤 메서드를 사용할 것인지 서버에게 알리기 위해 사용된다.
- Access-Control-Request-Headers
    - `preflight` 요청을 할 때 실제 요청에서 어떤 header를 사용할 것인지 서버에게 알리기 위해 사용된다.

### 응답 헤더 목록

- Access-Control-Allow-Origin
    - 브라우저가 해당 origin이 자원에 접근할 수 있도록 허용한다.
- Access-Control-Expose-Headers
    - 브라우저가 액세스할 수 있는 서버 화이트리스트 헤더를 허용한다.
- Access-Control-Max-Age
    - 얼마나 오랫동안 `preflight`요청이 캐싱 될 수 있는지를 나타낸다.
- Access-Control-Allow-Credentials
    - `Credentials`가 true 일 때 요청에 대한 응답이 노출될 수 있는지를 나타냅니다.
    - `preflight`요청에 대한 응답의 일부로 사용되는 경우 실제 자격 증명을 사용하여 실제 요청을 수행할 수 있는지를 나타냅니다.
    - 간단한 GET 요청은 `preflight`되지 않으므로 자격 증명이 있는 리소스를 요청하면 헤더가 리소스와 함께 반환되지 않으면 브라우저에서 응답을 무시하고 웹 콘텐츠로 반환하지 않습니다.
- Access-Control-Allow-Methods
    - preflight`요청에 대한 대한 응답으로 허용되는 메서드들을 나타냅니다.
- Access-Control-Allow-Headers
    - `preflight`요청에 대한 대한 응답으로 실제 요청 시 사용할 수 있는 HTTP 헤더를 나타냅니다.
     
---


# Spring Boot로 CORS 설정하기

### 1. Configuration 으로 해결하기

Global하게 적용하는 방법으로, config 패키지를 만들어준다.

경로는 /src/main/java/{project}/config 만들어진 config 패키지 안에 WebConfig 클래스를 만들어준다.

### 1.1. addMapping

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {
	@Override
	public void addCorsMappings(CorsRegistry registry) {
		registry.addMapping("/**");
	}
}
```

`registry.addMapping`을 이용해서 `CORS 적용할 URL 패턴`을 정의할 수 있다.

위 처럼  “/**” 와일드 카드를 사용할 수도 있다.

또한 Ant-style도 지원하며 “/somePath/**” 이렇게 적용할 수도 있다.

Default 값은 아래와 같다.

- Allow all origins.
- Allow “simple” methods GET, HEAD and POST
- Allow all headers
- Set max age to 1800 seconds (30 minutes).

### 1.2. allowedOrigins

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {
	@Override
	public void addCorsMappings(CorsRegistry registry) {
		registry.addMapping("/**")
						.allowedOrigins("*");
	}
}

.allowedOrigins("http://localhost:8080", "http://localhost:8081"); // 한 번에 여러 Method를 허용
```

allowedOrigins 메소드를 이용해서 자원 공유를 허락할 Origin을 지정할 수 있다.

“*”로 모든 Origin을 허락할 수 있다.

### 1.3. allowedMethods

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {
	@Override
	public void addCorsMappings(CorsRegistry registry) {
		registry.addMapping("/**")
						.allowedOrigins("*")
						.allowedMethods("GET", "POST");
	}
}
```

allowedMethods를 이용해서 허용할 HTTP method를 지정

### 1.4. maxAge

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {
	@Override
	public void addCorsMappings(CorsRegistry registry) {
		registry.addMapping("/**")
						.allowedOrigins("*")
						.allowedMethods("GET", "POST")
						.maxAge(3000);
	}
}
```

maxAge 메소드를 이용해서 원하는 시간만큼 pre-flight 리퀘스트를 캐싱 해둘 수 있다.

## 2. Annotation 이용하기

Controller 또는 메소드단에서 annotation을 통해 적용하는 방법

```java
@RequestMapping("/somePath")
@CrossOrigin(origins = "*", allowedHeaders = "*")
public class SomeController {
}

@RestController
@RequestMapping("/somePath")
public class SomeController {

    @CrossOrigin(origins="*")
    @RequestMapping(value = "/{something}",method = RequestMethod.DELETE)
    public ResponseEntity<String> delete(@PathVariable Long reservationNo) throws Exception{
    }

}
```

- CorssOrigin 어노테이션을 사용하면 global하게 설정하던 것 과 같이 허용할 origins이나 methods를 지정할 수 있다.
- origins, methods, maxAge, allowedHeaders를 사용할 수 있다.

[ref]<br>
[https://hannut91.github.io/blogs/infra/cors](https://hannut91.github.io/blogs/infra/cors) <br>
[https://dev-pengun.tistory.com/entry/Spring-Boot-CORS-설정하기](https://dev-pengun.tistory.com/entry/Spring-Boot-CORS-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0)