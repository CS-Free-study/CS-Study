# API

# API란?

> API(Application Programming Interface)는 프로그램에서 사용할 수 있도록 운영체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스

<br>

# API의 개념

- `프로그램 간`의 `중간 다리 역할`을 해준다.   
GUI(Graphic User Interface)와 CLI(Command Line Interface)가 사람과 프로그램 사이의 중간 다리 역할을 해주는 것과 비슷하다.
- API는 소스 코드 수준에서 정의되는 인터페이스라고 할 수 있다.
- function, method등의 이름으로 불리는 `소프트웨어 컴포넌트`의 기능이다.
- API 자체는 `사양`만을 정의하기 때문에 `구현`과는 독립적이다.   
실제로 구현한 것은 `라이브러리`라고 부른다.

<br>

## 쉽게 이해하는 API

![스크린샷 2022-07-08 02.07.06.png](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/network/images/API/Image.png)

1. `손님`은 `웨이터`를 불러 `음식`을 주문한다.   
→ `앱(웹)`은 `API`에게 A와 관련된 `데이터` 요청한다.
2. `웨이터`는 `셰프`에게 `음식`을 요청한다.   
→ `API`는 `운영체제`에게 `데이터`를 요청한다.
3. `셰프`는 요리가 끝난 후 `웨이터`에게 `음식`을 전달한다.   
→ `운영체제`는 `API`에게 `데이터`를 전달한다.
4. `웨이터`는 `손님`에게 주문한 `음식`을 제공한다.   
→ `API`는 `앱(웹)`에게 요청한 `데이터`를 제공한다.
- 손님 = 앱(웹) = 응용 프로그램   
웨이터 = API   
셰프 = 운영체제 or 서버 or 프로그래밍 언어   
음식 = 데이터

<br>

## 앱에서의 API 사용

```swift
private func networking<T: Decodable>(urlStr: String, method: HTTPMethod, data: Data?, model: T.Type, completion: @escaping(Result<T, AFError>, StatusCode) -> Void) {
    var statusCode: StatusCode = .fail
    guard let url = URL(string: Address.base.url + urlStr) else {
        print("URL을 찾을 수 없습니다.")
        return
    }
    
    var request = URLRequest(url: url)
    request.setValue("application/json", forHTTPHeaderField: "Content-Type")
    request.httpBody = data
    request.method = method
    
    AF.request(request)
        .validate(statusCode: 200..<500)
        .responseDecodable(of: model.self) { response in
            switch response.response?.statusCode {
            case 200: statusCode = .success
            case 500: statusCode = .server
            default: break
            }
            
            switch response.result {
            case .success(let result):
                completion(.success(result), statusCode)
            case .failure(let error):
                completion(.failure(error), statusCode)
            }
        }
}
```

- 현재 하고 있는 프로젝트의 일부
- networking()을 호출하면 데이터를 얻는다.
1. `앱`이 `API`에게 `데이터`를 요청   
→ 앱에서 T(데이터 모델)를 반환하는 networking() 호출
2. `API`는 `서버`에 `데이터`를 요청   
→ networking()를 통해 서버에 request
3. `서버`는 데이터베이스에서 `데이터`를 찾아 `API`에게 전달   
→ 서버에서 response에 데이터가 담겨옴
4. `API`는 `앱`에게 요청한 `데이터`를 전달   
→ networking()은 response에 담겨진 T를 반환

<br>

# API의 종류

### 오픈 API

> 누구나 쉽게 접근하여 정보를 공유하기 위해 만들어진 API
> 

### 비공개 API

> 권한이 있는 일부 사용자들에게만 정보를 제공하기 위해 만들어진 API
> 

### ★REST(ful) API★

> 개봉 박두
> 

<br>

# API의 장점

## 개인(개발자)

- C언어나 어셈블리어 같이 저단계 프로그래밍 언어에서나 할법한 메모리 / 하드웨어 조작 등을 직접할 필요 없이, API만을 가지고도 손쉽게 고레벨 프로그래밍 언어에서도 제어할 수 있다.
- 개발자는 배포된 API를 받고 이를 자신의 코드에 추가함으로써 원하는 기능을 구현할 수 있다.    
→ 운용중인 애플리케이션에 적법한 절차를 걸쳐 허락을 맡고 구현물을 받아오거나 새로운 요소를 삽입, 수정할 수 있는 것이다.

## 기업

### 외부 데이터를 사용하여 풍부한 사용자 경험 창출

- 사용자는 API가 어떻게 구현되어있는지 알지 못해도 API의 응답으로 오는 데이터를 안전하게 즉시 사용할 수 있다.
- 처음부터 개발하거나 유지보수할 필요가 없는 외부 데이터와 기능에 접속할 수 있다.

### 워크플로우를 개선하여 보유 사용자 증가

- 가게 정보나 위치같은 일정 데이터를 직접 구하여 나열하는 대신 Google Map API 등을 통해 한 번에 얻을 수 있다.
- 좋은 API를 통한 매끄러운 워크플로우는 사용자의 시간을 절약하고 플랫폼을 다시 사용할 이유를 제공한다.

### 유연한 애플리케이션 기능 개발

- 새로운 기능을 개발할 때, 처음부터 다시 개발하는 대신 API를 통하여 보존된 리소스를 이용할 수 있다.
- API는 애플리케이션과 서버를 분리하여 유지할 수 있도록 디자인되었기 때문에 서로 영향을 주지 않으면서 수정할 수 있다.

<br>

# 면접 질문

- API가 무엇인가요?
