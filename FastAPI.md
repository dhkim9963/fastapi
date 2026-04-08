# FastAPI는 

> 파이썬 언어를 위해 설계된 최신 웹 프레임워크로 API 개발에 최적화되어 있음     
비동기 프레임워크인 Starlette(스타레테)를 기반으로 웹 요청을 처리하며, 데이터 검증과 설정을 위해 Pydantic(파이단틱)라이브러리 사용함    
성능에 중점을 두고 있으며, 특히 '비동기(async)' 프로그래밍을 지원함으로써 I/O 작업이 많은 애플리케이션에서 빠른 처리 속도를 제공함      
RESTful API를 쉽게 구축할 수 있게 돕는 것이 가장 큰 장점    

## RESTful API는
> 웹 서비스에서 클라이언트와 서버 간에 데이터를 교환하는 데 사용되는 일반적인 방식   
FastAPI는 이러한 API를 구축할 때 필요한 많은 기본 설정과 보일러플레이트 코드를 줄여줌   

## 보일러플레이트 코드(boilerplate code)란
> 애플리케이션의 동작과 관련 없이 반복되어 작성되어야 하는 코드 조각들을 말함    
이러한 코드는 대부분의 프로그래밍 작업에서 일반적으로 필요한 기본적인 설정이나 준비 작업을 수행하기 위해 사용됨     
다른 파이썬 웹 프레임워크인 플라스크와 비교했을 때 플라스크는 간단하고 직관적이지만 기본적으로 '동기(sync)'처리를 기반으로 하고 있음       
동기 처리는 한 번에 하나의 작업만 처리할 수 있어서 I/O 바운드 작업이 많은 애플리케이션에서는 FastAPI가 제공하는 비동기 처리 방식이 더 효율적일 수 있음      

### _요약하면 FastAPI는 비동기 처리를 강력하게 지원하며 빠르고 효율적인 API 개발을 위한 현대적인 기능들을 제공하는 파이썬 웹 프레임워크_

## FastAPI의 장점
>1. 성능    
    FastAPI는 매우 빠른 웹 프레임워크이며 비동기 처리에 최적화 되어 있어 I/O바운드 작업에서 더 빠름
>2. 자동 문서화     
    FastAPI는 API만 작성하면 별도의 확장 기능 없이도 자동으로 API문서를 생성함
>3. 쉬운 유효성 검사    
    FastAPI는 Pydantic 라이브러리를 활용하여 데이터 유효성 검사를 간단히 수행할 수 있음
>4. 비동기 프로그래밍   
    FastAPI는 비동기 작업을 간단히 처리할 수 있음

## FastAPI 실습
## FastAPI를 사용하기 위해 콘다 가상환경 설정
```
conda create fastapi python=3.10.14
conda activate fastapi
conda install fastapi
conda install uvicorn
```

## fastapi 테스트 코드
```python
# main.py 
from fastapi import FastAPI # FastAPI 라이브러리 import

app = FastAPI() # FastAPI instance 생성

@app.get("/") # HTTP GET 요청을 "/" 경로로 받을 준비
def read_root(): # 요청을 처리할 함수를 정의
    return {"message":"Hello, world!"} # JSON 형태의 응답을 반환
```

## 실행문
> ```
> uvicorn main:app --reload
> ```
> * main : FastAPI 애플리케이션 코드가 작성된 파이썬 파일의 이름을 의미함(main.py 파일 내에 있다고 가정)   
> * app : FastAPI 인스턴스를 생성하는 객체의 변수 이름을 가리킴(즉, app = FastAPI()라고 정의된 경우)   
> * --reload : 이 옵션은 개발중에 코드를 수정할 때마다 서버가 자동으로 재시작하도록 설정하여 코드 변경 사항이 바로 적용되도록 함(빠르고 효율적인 개발과정)
   
## 자동 문서화
> 개발자가 API를 개발하고 나면, 이 API가 어떻게 동작하는지를 문서화함   
> 이 과정은 시간이 많이 들고, 자주 업데이트해야 하는 문제가 존재함   
> Fast API를 사용하면 코드에 작성된 타입 힌트(type hint)와 함께 추가적인 데코레이터나 매개변수를 통해 API에 대한 문서를 자동으로 생성함   
> 예를 들어 예제에서 @app.get("/")라는 라우터를 정의했다면 FastAPI는 이 정보를 바탕으로 해당 API 엔드포인트(endpoint)에 대한 문서를 자동으로 생성함
>* 시간 절약 : 수동으로 문서를 업데이트할 필요가 없으므로, 개발에 더 많은 시간을 쏟을 수 있음
>* 항상 최신 정보 유지 : 코드가 업데이트되면 문서도 자동으로 업데이트되므로, 문서가 오래되어 무용지물이 되는 일이 없음
>* API 테스트 : Swagger UI 또는 리독에서 직접 API를 호출하여 테스트할 수 있음
>* 타입 검사와 유효성 검증 : 문서를 생성할 때 FastAPI는 코드에 명시된 타입힌트와 유효성 검사 규칙을 참고하여 문서에 반영함  

***
***
# 라우팅

## 기본 라우팅
> 가장 간단한 형태의 라우팅은 HTTP GET 메서드를 사용하는 경우 
> 아래 예시는 루트 URL(http://127.0.0.1:8000/)에 GET 요청을 하면 "Hello, FastAPI"라는 응답을 보내는 예시
```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message" : "Hello, FastAPI"}
```

## 경로 매개변수
> FastAPI는 사용자의 요청을 구체적으로 명시하기 위해 <u>경로 매개변수</u>와 <u>쿼리 매개변수</u>라는 두 가지 종류의 매개변수를 사용하며 두 용어는 경로 파라미터와 쿼리 파라미터로도 불림   
> 경로 매개변수는 URL의 특정 부분을 변수로써 사용하여 동적으로 변할 수 있는 값을 처리할 때 사용함    
> 이 매개변수들은 URL의 구조 안에 직접 포함되어 있기 때문에 경로의 일부로 인식됨 
> 예를 들어, /item/1과 /item/2라는 URL에서 1과 2는 각각 다른 아이템을 식별하는 고유한 값으로, 경로 매개변수 item_id를 통해 서버에 전달됨
```python
@app.get("/items/{item_id}")
def read_item(item_id):
    return{"item_id" : item_id}
```
> 위 코드에서 {item_id}는 경로 매개변수를 정의하는 부분으로, 사용자가 방문하는 URL의 해당 부분에 있는 값을 int타입으로 rea_item()함수에 전달함   

> FastAPI를 사용하여 여러 개의 경로 매개변수를 포함하는 라우트를 만들 때, URL의 여러 부분을 동적으로 캡처하여 함수에 전달할 수 있음     
> 예를 들어 사용자가 /users/123/items/foobar와 같은 URL에 액세스하는 경우, 여기에는 두 개의 경로 매개변수가 있음    
> 하나는 <u>사용자 식별자(user_id)</u>이고 다른 하나는 <u>아이템 이름(item_name)</u>    
> 복수의 경로 매개변수를 사용하지 않는 경우의 예시 코드는 다음과 같음
```python
from fastapi import FastAPI

app = FastAPI()
@app.get("/users/{user_id}/items/{item_name}")
def read_user_item(user_id, item_name):
    # 여기서 user_id와 item_name은 문자열로 전달됨
    return {"user_id" : user_id, "item_name" : item_name}
```
> 이 예시에서 사용자가 /users/123/items/foobar URL로 요청을 보낼 때, 123은 user_id로, foobar는 item_name으로 각각 함수의 매개변수로 전달됨  
> FastAPI는 기본적으로 경로 매개변수를 문자열로 처리함  

> 복수의 경로 매개변수를 사용하는 것은 웹 API에서 매우 일반적이며, 이를 통해 클라이언트는 서버에 특정 자원을 정확하게 요청할 수 있음    
> 서버는 이 정보를 사용하여 요청받은 자원을 찾아 응답할 수 있음 
> 이 방식은 URL 경로의 의미를 더욱 명확하게 하고, 웹서비스의 구조를 이해하기 쉽게 만듦

## 쿼리 매개변수
> 쿼리 매개변수는 URL의 경로 이후 ?로 시작되는 부분에 정의되며, 키-값 싸으이 형태로 정보를 전달하는 데 사용됨   
> 이 매개변수들은 주로 필터링, 정렬, 페이지네이션 등과 같이 요청을 더 세부적으로 조정할 필요가 있을 때 활용됨   
> 쿼리 매개변수는 선택적이며, 동일한 경로에 대해서 다양한 연산을 가능하게 함
```python
@app.get("/items/")
def read_items(skip, limit):
    return {"skip" : skip, "limit" : limit}
```
> 위 예시에서 skip과 limit 매개변수는 쿼리 매개변수 
> 사용자가 /items/?skip=5&limit=5와 같이 요청을 보내면, 서버는 이를 해석하여 skip과 limit에 해당하는 값을 함수의 매개변수로 사용함  

> 쿼리 매개변수는 다음 두 코드와 같이 작성할 수 있음    
> 두 코드 사이의 주요 차이점은 매개변수의 기본값 설정에 있음    
> * 첫 번째 코드에서는 skip과 limit 매개변수에 기본값이 설정되어 있지 않음
```python
@app.get("/items/")
def read_items(skip, limit):
    return {"skip" : skip, "limit" : limit}
```
> 이는 클라이언트가 이 매개변수들을 반드시 URL 쿼리에 포함하여 값을 제공해야 함을 의미함    
> 예를 들어, /items/?skip=5&limit=5처럼 매개변수값을 명시적으로 지정하지 않으면, FastAPI는 에러를 반환함    

> * 두 번째 코드에서는 skip과 limit 매개변수에 기본값이 설정되어 있음
```python
@app.get("/items/")
def read_items(skip = 0, limit = 10):
    return{"skip" : skiip, "limit" : limit}
```
> 즉, 클라이언트가 이 값들을 제공하지 않아도 기본값인 0과 10이 사용됨   
> 이는 클라이언트가 매개변수를 생략해도 요청이 성공하며, 서버는 기본 설정된 값으로 응답을 반환함

> 경로 매개변수와 쿼리 매개변수는 이처럼 각각 URL의 경로와 쿼리 스트링으로부터 정보를 수집하는 역할을 함    
> FastAPI는 이 두 가지 매개변수를 명확하게 구분하여 사용함으로써 API의 정확성과 편의성을 향상시킴   

## curl을 사용한 테스트
> 지금까지의 라우팅 코드를 모아서 FastAPI 코드를 작성하고 실행함
```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message" : "Hello, FastAPI"}

@app.get("items/{item_id}")
def read_item(item_id):
    return{"item_id" : item_id}

@app.get("/items/")
def read_items(skip = 0, limit = 10):
    return {"skip" : skip, "limit" : limit}
```
> 이 코드를 main.py에 저장한 후 터미널에서 다음과 같이 실행함
```
uvicorn main:app --reload
```
> curl은 Client URL의 약자로, 다양한 프로토콜을 지원하는 명령행 기반의 네트워크 도구    
> 주로 웹 서버와의 상호작용을 위해 사용되며 HTTP, HTTPS, FTP 등 다양한 프로토콜을 지원함    

***
***

# 타입 힌트
> 타입 힌트(type hint)는 프로그래밍에서 변수나 함수의 예상 타입을 명시적으로 표시하는 기술   
> FastAPI는 파이썬의 타입 힌트를 사용하여 요청을 검증하고, 적절한 데이터가 요청과 응답에 사용되도록 도움    
> 이 기능을 통해 개발자는 별도의 검증 로직을 작성하지 않고도 안정적인 API를 구축할 수 있음

## 기본 타입 힌트
> FastAPI에서 경로 매개변수나 쿼리 매개변수에 타입 힌트를 추가하면, 해당 타입에 맞지 않는 요청은 자동으로 거부됨    
> 또한, 매개변수에 기본값을 설정하여 선택적으로 만들 수 있음
```python
# main.py
from fastapi import FastAPI

app = FastAPI()

# 경로 매개변수 사용 예제
@app.get("/items/{item_id}")
def read_item(item_id: int): # q는 기본값이 None인 쿼리 매개변수
    return {"item_id" : item_id}

# 쿼리 매개변수 사용 예제
@app.get("/getdata/")
def read_items(data: str = "funcoding"): # data의 기본값은 'funcoding'
    return {"data" : data}

# 실행 : uvicorn main:app --reload
```

## 고급 타입 힌트
> FastAPI는 typing 모듈에서 제공하는 List, Dict 같은 고급 타입 힌트를 사용하여 요청 데이터를 쉽게 다룰 수 있음
```python
# main.py
from fastapi import FastAPI, Query
from typing import List, Dict

app = FastAPI()

# List 데이터 타입을 쿼리 매개변수로 받는 라우트 예제
@app.get("/items/")
def read_items(q: List[int] = Query([])): # 빈 리스트를 기본값으로 설정
    return {"q" : q}

# Dict 데이터 타입을 요청 바디로 받는 라우트 예제
@app.post("/create-item/")
def create_item(item : Dict[str, int]):
    return item
```
> Query는 쿼리 매개변수의 기본값을 설정하는 데 사용되며, 유효성 검사 및 메타데이터 선언에도 사용됨  
> 여기서 Query([])는 해당 쿼리 매개변수가 필수가 아님을 나타내고, 기본값으로 빈 리스트를 제공함 
> Dict와는 달리 List 타입 힌트의 경우에는 List[int] = Query([])와 같이 반드시 Query() 관련 구문을 함께 넣어주어야 타입 힌트 유효성 검사가 정상 동작함   

## 타입 힌트로 사용 가능한 데이터 타입
> * 기본 데이터 타입
>   + int : 정수
>   + float : 부동소수점 숫자
>   + str : 문자열
>   + bool : 불리언(True or False)

> * 컬렉션 타입
>   + List : 변경 가능한 순서가 있는 컬렉션     
            - e.g. List[int]는 정수의 리스트를 나타냄
>   + Tuple : 변경 불가능한 순서가 있는 컬렉션      
            - e.g. Tuple[str, int]는 문자열과 정수의 튜플을 나타냄
>   + Dict : 키와 값의 쌍을 갖는 컬렉션     
            - e.g. Dict[str, float]는 문자열 키와 부동소수점 숫자 값의 딕셔너리를 나타냄
>   + set : 중복 없는 항목의 컬렉션     
            - e.g. Set[bool]은 불리언 값의 세트를 나타냄

> * 특수 타입
>   + None : 아무런 값을 갖지 않음을 나타냄
>   + Any : 모든 타입을 허용, 타입 검사를 무시하고자 할 때 사용

> * typing 모듈의 고급 타입
>   + Optional : 값이 있거나 None일 수 있는 타입    
            - e.g. Optional[str]은 문자열이거나 None일 수 있음
>   + Union : 여러 타입 중 하나일 수 있는 값    
            - e.g. Union[int, str]은 정수 또는 문자열이 될 수 있음
>   + Callable : 호출 가능한 객체(함수 등)를 나타냄     
            - e.g. Callable[[int, int], int]는 두 정수 매개변수를 받고 정수를 반환하는 함수
>   + Iterable : 반복 가능한 객체를 나타냄      
            - e.g. Iterable[str]은 문자열을 항목으로 갖는 반복 가능 객체
>   + Sequence : 시퀀스 타입을 나타냄       
            - e.g. Sequence[float]는 부동소수점 숫자의 시퀀스

> * 사용자 정의 타입
>   + 클래스타 나들 타입 힌트를 사용하여 사용자 정의 타입을 생성할 수 있음      
            - e.g. 클래스 Person을 정의하고 def get_person() -> Person: 과 같이 사용할 수 있음

> 이러한 타입은 단독으로 사용하거나 typing 모듈의 다양한 기능과 결합하여 더 복잡한 타입 힌트를 만드는 데 사용할 수 있음     
> 예를 들어 List[Dict[str, Union[int, str]]]은 문자열을 키로 하고 정수 또는 문자열을 값으로 하는 딕셔너리의 리스트를 나타냄     
> FastAPI는 이러한 타입 힌트를 사용하여 요청에서 받은 데이터의 형식을 검증하고, 응답 데이터를 적절한 형식으로 변환하며 API에 대한 문서를 자동으로 생성함

***
***

# HTTP 메서드
> HTTP 메서드는 클라이언트가 서버에게 어떤 동작을 해달라고 요청하는 방식을 정의함   
> FastAPI는 이러한 메서드를 사용하여 요청의 의도를 명확히 하고, 적절한 엔드포인트에 연결하는 라우팅을 수행함    
> * GET
>   > 이 메서드는 서버로부터 정보를 요청할 때 사용함    
>   > 데이터를 가져오는 read-only 작업에 적합하며, 서버의 상태나 데이터를 변경하지 않음
>   > 예를 들어 사용자의 프로필 데이터나 게시글 목록을 가져올 때 GET 요청을 사용함
> * POST
>   > 서버에 데이터를 전송하여 새로운 리소스를 생성하려고 할 때 POST 메서드를 사용함    
>   > 예를 들어 새 사용자를 등록하거나 게시글을 작성할 때 사용함    
>   > POST 요청은 데이터를 서버의 특정 경로에 제출하며, 해당 데이터는 주로 요청 바디에 포함됨   
> * PUT
>   > PUT 메서드는 지정된 리소스의 전체 업데이트를 수행함   
>   > 예를 들어, 사용자의 전체 프로필을 업데이트하는 경우에 PUT 요청을 사용할 수 있음   
>   > PUT은 리소스가 존재하지 않는 경우 새로 생성할 수도 있지만, 주로 기존 리소스의 완전한 교체를 의미함    
> * DELETE
>   > DELETE 메서드는 지정된 리소스를 삭제할 때 사용함  
>   > 이 요청은 서버에 리소스의 제거를 지시하며, 성공적으로 처리된 경우 리소스에 더 이상 접근할 수 없음     
>   > 예를 들어, 사용자가 자신의 계정을 삭제하거나 작성한 게시글을 제거하고 싶을 때 DELETE 요청을 사용할 수 있음

> FastAPI를 사용하면 이러한 메서드를 각각의 라우팅 데코레이터(@app.get(), @app.post(), @app.put(), @app.delete() 등)와 함께 사용하여 다양한 HTTP 요청을 처리하는 API를 손쉽게 구성할 수 있음

## FastAPI 코드 작성
```python
# main.py
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message" : "Hello, FastAPI"}

@app.get("/items/{item_id}")
def read_item(item_id : int):
    return {"item_id" : item_id}

@app.get("/items/")
def read_items(skip: int=0, limit: int=10):
    return {"skip" : skip, "limit" : limit}

@app.post("/items")
def create_item(item: dict):
    return {"item" : item}

@app.put("/items/{item_id}")
def update_item(item_id: int, item: dict):
    return {"item_id": item_id, "update_item":item}

@app.delete("/items/{item_id}")
def delete_item(item_id: int):
    return{"message" : f"Item {item_id} has been deleted"}
```

## curl을 사용한 테스트
### POST 메서드 테스트
> 새 아이템을 생성함    
> 아이템은 JSON 형태로 전달됨   
> FastAPI에서는 요청바디로부터 데이터를 받기 위해 반드시 Pydantic 모델을 사용해야 하는 것은 아니지만, Pydantic 모델을 사용하는 것을 권장함      
> POST 메서드는 데이터를 요청 바디에 넣어서 전송하므로 해당 데이터 처리를 위해서는 Pydantic 모델을 고려할 수 있음   
> 다만 해당 모델을 익히기 전이므로 위 코드는 직접 파이썬의 내장 dict 타입을 사용함      
> 파이썬의 내장 dict 타입을 직접 사용하면 Pydantic은 요청 바디가 JSON 형식이라는 것만을 기대하고, 그 내용에 대해서는 검증을 수행하지 않음   
> curl 명령에서 -d 옵션을 사용할 때 Content-Type 헤더를 지정하지 않으면 기본적으로 application/x-www-form-urlencoded로 설정됨   
> 그래서 이 경우에는 -H "Content-Type: application/json" 헤더를 추가해야 함     
> 이렇게 하면 curl이 데이터를 JSON으로 보내고 FastAPI가 이를 dict로 변환하여 정상 동작할 수 있음
```
curl -X POST "http://127.0.0.1:8000/items" -H "Content-Type: application/json" -d "{\"name\":\"item1\", \"value\":42}"
```

### PUT 메서드 테스트
> 아이템 ID가 1인 아이템의 정보를 업데이트함
```
curl -X PUT "http://127.0.0.1:8000/items/1" -H "Content-Type: application/json" -d "{\"name\":\"update_item\", \"value\":43}"
```

### DELETE 메서드 테스트
> 아이템 ID가 1인 아이템을 삭제함
```
curl -X DELETE "http://127.0.0.1:8000/items/1" -H "Content-Type: application/json"
```

***
***

# Pydantic
> FastAPI에서 Pydantic(파이단틱)은 데이터 검증과 데이터 직렬화를 쉽게 만들어줌  
> 먼저 <u>데이터 검증</u>과 <u>데이터 직렬화</u>가 무엇인지 알아봄  

> * 데이터 검증(data validation)
>   > 사용자나 다른 시스템이 보내는 데이터가 올바른 형식과 값인지 확인하는 과정     
>   > 예를 들어, 사용자가 금액을 입력할 때 문자열을 넣으면 이는 올바르지 않은 데이터임      
>   > 데이터 검증을 통해 이런 잘못된 정보를 사전에 차단할 수 있음       
> * 데이터 직렬화(data serialization)
>   > 복잡한 데이터 구조를 바이트나 문자열로 변환해서 다른 시스템과 쉽게 데이터를 교환할 수 있는 형태로 만드는 것       
>   > 반대 과정을 '역직렬화'라고 하며, 이는 문자열이나 바이트를 원래의 데이터 구조로 되돌리는 것    

> 데이터 검증과 데이터 직렬화는 다음과 같은 이유로 필요함
>   > <b>데이터 검증</b> : 잘못된 데이터가 처리되는 것을 막아서 버그나 다양한 문제를 예방함     
>   > <b>데이터 직렬화</b> : 서로 다른 시스템끼리 데이터를 쉽게 주고받을 수 있게 해줌       

> 특히 FastAPI에서는 요청 바디로부터 데이터를 받기 위해 반드시 Pydantic 모델을 사용해야 하는 것은 아니지만, Pydantic 모델을 사용하는 것을 권장함    
> 데이터 요청을 위해 자주 사용하는 HTTP POST 메서드는 데이터를 요청 바디에 넣어서 전송하므로, POST 메서드로 API를 선언하는 경우에는 Pydantic 모델 사용을 고려해야함     

## Pydantic 모델 적용




