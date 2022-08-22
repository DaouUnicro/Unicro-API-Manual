**인증체크**
----
API호출시 필수값인 토큰발급을 위해 사용하는 API입니다.

* **기능**
  인증발급

* **URI**
  /users/auth

* **Method:**
  `POST`

*  **URL Params**

| 파라메터 | 설명 | 타입 | 필수 |
|--|--|--|--|
| unicroUserNo|유니크로 사용자 식별키로 유니크로 가입후 전달 한 값입니다. | Integer | O |
| userId|유니크로 아이디| String (4~75 byte 영문소문자, 숫자, @ _ . 만 가능(공백불가)) | O |
 
* **응답:**
 
```json
{
  "result": "SUCCESS",
  "msg": "토큰 발급을 성공했습니다.",
  "errorCd": "",
  "data": {
    "unicroToken": "ABCDEFG"
  }
}

```

