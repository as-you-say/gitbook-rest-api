# gitbook-rest-api

## HTTP 상태코드

RestAPI 관련 문서

| No | 코드 | 설 | 요청 |
| :---: | :---: | :--- | :---: |
| 1 | 200 | 성공 | ALL |
| 2 | 201 | 추가 요청시 정상적으로 추가 | POST |
| 3 | 204 | 삭제 요청시 해당 데이터가 없음 | DELETE |
| 4 | 304 | 수정 요청 수정되지 않음 | PUT |
| 5 | 400 | 잘못된 요청 - 파라미터가 올바르지 않은 경 | ALL |
| 6 | 401 | 인증 실패 - 토큰이나 계정에 대한 세션 만료인 경 | ALL |
| 7 | 403 | 권한이 없음 - 해당 계정의 권한으로 접근할 수 없는 자원 | ALL |
| 8 | 404 | 찾을수 없음 - 잘못된 URL로 이동하거나, 잘못된 URL의 자원을 참조하는 경 | ALL |
| 9 | 409 | 충돌 - 서비스 로직상의 모순이 발생하여 충돌이 일어난 경 | PUT |
| 10 | 500 | 서버 에러 - 웹 서비스 자체의 에러가 발생한 경우 \(서버의 로그확인 필요\) | ALL |

## JQuery AJAX

### 1. 코드 작성방법

```javascript
$.ajax({
    url: '',
    method: 'GET or POST or PUT or DELETE',
    contentType: '',
    dataType: '',
    data: { ... },
    async: true or false,
    success: function (value) { ... },
    error: function (error) { ... }
})
```

### 

### 2. 필요한 파라미터

| No | Name | Data Type | Description |
| :---: | :---: | :---: | :--- |
| 1 | url | string | 요청을 보낼 URL 주소 |
| 2 | method | string | HTTP 요청 방식 |
| 3 | contentType | string | 서버가 받을 데이터의 타입 |
| 4 | dataType | string | 서버로부터 받을 데이터 타입 |
| 5 | data | object | 요청을 보낼 URL 에 필요한 파라미터를 담아서 보내주는  |
| 6 | async | boolean | 비동기 처리 여부 \(동기: false, 비동기: true\) |
| 7 | success | function | 요청이 성공할 시 실행되 함수 |
| 8 | error | function | 요청이 실패할 시 실행되는 함수 |

### 

### 3. 에러 정보 출력하기

<table>
  <thead>
    <tr>
      <th style="text-align:center">No</th>
      <th style="text-align:center">&#xC18D;&#xC131;&#xBA85;</th>
      <th style="text-align:left">&#xB0B4;&#xC6A9;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:center">1</td>
      <td style="text-align:center">status</td>
      <td style="text-align:left">&#xC5D0;&#xB7EC; &#xCF54;&#xB4DC; (4xx, 5xx)</td>
    </tr>
    <tr>
      <td style="text-align:center">2</td>
      <td style="text-align:center">statusText</td>
      <td style="text-align:left">&#xC5D0;&#xB7EC; &#xBA54;&#xC2DC;&#xC9C0; (Internal Server Error ...)</td>
    </tr>
    <tr>
      <td style="text-align:center">3</td>
      <td style="text-align:center">readyState</td>
      <td style="text-align:left">
        <p>&#xC5D0;&#xB7EC;&#xAC00; &#xBC1C;&#xC0DD;&#xD55C; &#xC2DC;&#xC810;</p>
        <ul>
          <li>0 : &#xC694;&#xCCAD;&#xC774; &#xC900;&#xBE44;&#xB418;&#xAE30; &#xC804;</li>
          <li>1 : &#xC11C;&#xBC84; &#xC5F0;&#xACB0;&#xC774; &#xC131;&#xB9BD;&#xB41C;
            &#xC2DC;</li>
          <li>2 : &#xC11C;&#xBC84;&#xAC00; &#xC694;&#xCCAD;&#xC744; &#xBC1B;&#xC740;
            &#xC2DC;</li>
          <li>3 : &#xC11C;&#xBC84;&#xC758; &#xC791;&#xC5C5;&#xC774; &#xC218;&#xD589;&#xB418;&#xB294;
            &#xC2DC;</li>
          <li>4 : &#xC11C;&#xBC84;&#xC758; &#xC791;&#xC5C5; &#xC644;&#xB8CC; &#xD6C4;,
            &#xC751;&#xB2F5;&#xC5D0; &#xB300;&#xD55C; &#xC900;&#xBE44;&#xAC00; &#xC644;&#xB8CC;&#xB41C;
            &#xC2DC;</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

```javascript
$.ajax({
  ...
  error:function(error){
      // error 객체의 정보
      // - error.status
      // - error.statusText
      // - error.readyState
  }
})
```

## HTTP 모듈

### 1. 모듈 만들기

option 은 AJAX 의 기본적인 파라미터를 의미합니다. url / method / dataType / data / success / error 등이 있습니다.

baseUrl 은 http://api.sample.com/users,  http://api.sample.com/user/1 과 같이 쓰이는 경우에 http://api.sample.com 이라는 공통 url 주소를 의미합니다.

ajax 함수는 공통부분을 따로 빼서 정의하였고, ajax 함수를 구체적으로 정의한 get / post / put / delete 함수를 public 함수로 정의하여 외부에서 REST API 형태로 이용할 수 있도록 작성하였습니다.

| No | Name | Variable | Description |
| :---: | :---: | :---: | :--- |
| 1 | 매개변수 | options | AJAX 파라미터 \(url, method, dataType ...\) |
| 2 | 지역변수 | baseUrl | API의 기본 URL 주소 \(**http://api.sample.com/**users\) |
| 3 | private 함수 | ajax | ajax 함수의 공통부분만 따로 정의한 private 함수 |
| 4 | public  함수 | get, post, put, delete | ajax 함수를 구체적으로 정의한 public 함수 |

```javascript
var Http = function(options){
    var baseUrl = options.baseUrl;

    function ajax(url, data){
        options.url = baseUrl + url;
        options.data = data;
        return {
            then: function(success){
                options.success = success;
                return {
                    catch: function(error){
                    options.error = error;
                    $.ajax(options);
                }
            }
        }
    }
    
    return {
        get:function(url, data, async){
            options.async = (async === undefined) ? false : async;
            options.method = 'GET';
            return ajax(url, data);
        },
        post:function(url, data, async){
            options.async = (async === undefined) ? false : async;
            options.method = 'POST';
            return ajax(url, data);
        },
        put:function(url, data, async){
            options.async = (async === undefined) ? false : async;
            options.method = 'PUT';
            return ajax(url, data);
        },
        delete:function(url, data, async){
            options.async = (async === undefined) ? false : async;
            options.method = 'DELETE';
            return ajax(url, data);
        }
    }
}
```



### 2. 모듈 인스턴스 만들기

Bearer 토큰을 사용하는 날씨 API 가 있다고 가정을 한 후, 예시로 인스턴스를 만들어 보았습니다.

```javascript
var WEATHER = new Http({
  baseUrl:'https://apis.weather.com/',
  method:'',
  async:false,
  contentType: "application/json",
  dataType: 'json',
  data: {},
  beforeSend: function(req) {
    req.setRequestHeader('Authorization', 'Bearer ' + WEATHER_CSRF_TOKEN);
  },
  success: function(e){},
  error: function(e){}
});
```

### 

### 3. 모듈 인스턴스 사용하기

```javascript
WEATHER.get('/weather/list', { limit: 10 }, true)
.then(function(value){})
.catch(function(error){});

WEATHER.post('/weather/10', { temperature: '20' }, false)
.then(function(value){})
.catch(function(error){});

WEATHER.put('/weather/10', { temperature: '20' }, false)
.then(function(value){})
.catch(function(error){});

WEATHER.delete('/weather', { id:100 }, false)
.then(function(value){})
.catch(function(error){});
```

### 

### 4. OAuth2 인증 사용방법

모든 요청이 쿠키와 함께 가기 때문에, Server 측에서 Client 로 전달하는 쿠키를 읽을 수 없고, 수정할 수 없도록 옵션을 준 다음, 웹 브라우저에 리턴합니다.

따라서 모든 요청을 할 때마다 쿠키에 있는 토큰을 읽어들여서 해당하는 인증정보를 가지고 있는지 검증합니다. 쿠키가 가지고 있는 인증 정보는 사용자의 아이디와 이름을 포함하는 기타 정보들이 있습니다.

JWT 를 이용하여 토큰이 보유하고 있는 사용자 정보와 웹서버의 세션이 가지고 있는 사용자 정보의 일치여부를 확인하여 요정의 권한을 검증하게 됩니다.

초기에 오픈 API 프로세스는 아래와 같습니다.

{% hint style="info" %}
**웹서비스 OPEN API - 웹서비스와 사업자와 사용자 사이의 프로세스**  
1. 오픈 API를 제공하는 웹서비스의 홈페이지에서 사업자 아이디로 회원가입  
  
2. 해당하는 아이피만 허용하도록 API 이용자 정보를 등록 \(트래픽 당 요금이 발생하는 경우가 많기에 필수\)  
  
3. 등록이 완료되면 바로 제공되는 클라이언트 키 / 시크릿 키 값을 별도로 저장  
  
4. 프로젝트의 보안상 안전한 폴더에 키 파일을 보관 후 읽어와서 이용할 수 있도록 함 \(properties/yml\)  
  
5. 클라이언트 키와 시크릿 키를 이용하여 접속한 사용자에게 사용자가 가입되어있는 웹서비스의 개인정보에 대한 접근권한을 허용해달라는 팝업창을 띄우는 코드를 작성  
  
6. 사용자가 사업자의 프로젝트에 로그인 후, 사용자가 이용하고있는 웹 서비스의 정보를 사업자의 프로젝트에서 접근할 수 있도록, 동의를 구하는 링크또는 팝업으로 이동  
  
7. 권한 허용 버튼을 클릭  
  
8. 사업자의 프로젝트서버는 사용자의 정보에 대해 접근할 수 있는 엑세스 토큰과 리프레시 토큰을 발급받음  
  
9. 엑세스 토큰과, 리프레시 토큰을 사업자 프로젝트의 데이터베이스에 보관  
\(이 때, 리프레시 토큰이 있는 경우에는 엑세스 토큰의 만료기간이 있는 경우입니다. 따라서 리프레시 토큰이 없을 수도 있습니다. - 정책에 따라서 달리 사용됨.\)  
  
10. 사용자는 사업자 프로젝트를 이용할 때마다 본인이 허용했던 다른 웹 서비스의 정보를 함께 이용할 수 있음  
  
**!!!!!! 중요  
웹서비스 - OPEN API 제공  
통합 포탈 사이트\(SSO\) - 다양한 웹 서비스의 데이터를 가지고 화면을 보여줌  
사용자 - 기존에 여러개의 웹 서비스를 이용하고 있지만, 통합 포탈 사이트가 내가 필요로하는 웹 서비스들을 동시에 관리해주고, 원하는 모습으로 보여주고 있기 때문에 마음에 들어서 통합 포탈 사이트에 가입 후, 내가 사용하는 웹 서비스의 권한을 허용해서 한번에 보면서 관리하고 싶은 사람**
{% endhint %}



### 5. OPEN API 등록 후 사용방법

포탈 사이트 회원가입  
포탈 사이트 로그인  
웹서비스 허용권한 요청팝업  
웹서비스 허용권한 승인  
포탈 사이트 백엔드에서 웹 서비스에서 발급받은 토큰을 가져와서 디비에 저장  
\(이 방법은, 허용 권한 승인 후, 엑세스토큰을 https://포탈사이트.co.kr/callback?token=XXXX형식으로 리다이렉트 하면, 이 데이터만 쏙 빼서 디비에 저장 후에 바로 메인화면으로 이동해버린다. 오키?\)   
이제 포탈사이트 로그인 시에 디비에 있는 토큰을 가지고 요청을 전송  


