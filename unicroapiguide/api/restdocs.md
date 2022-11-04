# 제휴사 API

### 1. 인증 <a href="#_1_" id="_1_"></a>

#### 1.1 사용자 인증 토큰 발급 <a href="#_1_1_-_-_-_" id="_1_1_-_-_-_"></a>

***

API 호출시 헤더에 필수값인 사용자 인증 토큰 발급을 위해 사용하는 API입니다. 인증 토큰은 정상(NORMAL) 상태의 회원만 발급 가능합니다. 회원의 상태 확인은 2.1 회원 상태 조회 API를 통해 가능합니다.

* **기능** 사용자 인증 토큰 발급
* **URI** _/api/v1/auth_
* **Method:** `POST`

```
$ curl 'https://dev-api.unicro.co.kr:14147/api/v1/auth' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1' \
    -H 'Accept: application/json' \
    -d '{
  "partnerUserId" : "heesu",
  "unicroUserKey" : "$2a$10$WrUKHrgLHm3xoax6jGT1i.tAs29CLWTILPMgsZbpO5HyzMH7bQTHq"
}'
```

**요청**

```
POST /api/v1/auth HTTP/1.1
Content-Type: application/json
Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1
Accept: application/json
Content-Length: 118
Host: dev-api.unicro.co.kr:14147

{
  "partnerUserId" : "heesu",
  "unicroUserKey" : "$2a$10$WrUKHrgLHm3xoax6jGT1i.tAs29CLWTILPMgsZbpO5HyzMH7bQTHq"
}
```

**Request Fields**

| 필드명           | 타입     | 설명           | 필수값  | 제한                           |
| ------------- | ------ | ------------ | ---- | ---------------------------- |
| partnerUserId | String | 제휴사 사용자 아이디  | true | 4\~16자, 영문 소문자, 숫자만 가능, 공백불가 |
| unicroUserKey | String | 유니크로 사용자 식별키 | true |                              |

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 341

{
  "result" : "SUCCESS",
  "msg" : "사용자 인증 토큰 발급에 성공했습니다.",
  "errorCd" : "",
  "data" : {
    "unicroUserToken" : "eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY3NTUwNzAzfQ.dHsbMOeWZKR-Hp7OSALz0x6Prip3UxzdmP01XWBsE1WCTnc6CfwMd6eWwOLxzgsVFlgb4CgXEZu9UzmMmwKDSw"
  }
}
```

**Response Fields**

| 필드명                  | 타입     | 설명                                 |
| -------------------- | ------ | ---------------------------------- |
| result               | String | 성공실패 여부 코드 (성공: SUCCESS, 실패: FAIL) |
| msg                  | String | 응답 메시지                             |
| errorCd              | String | 실패시 에러 코드                          |
| data.unicroUserToken | String | 유니크로 사용자 인증 토큰                     |

### 2. 회원 <a href="#_2_" id="_2_"></a>

#### 2.1 회원 상태 조회 <a href="#_2_1_-_-_" id="_2_1_-_-_"></a>

***

유니크로 회원 상태를 조회하는 API입니다.

* **기능** 회원 상태 조회
* **URI** _/api/v1/users/{partnerUserId}/status_
* **Method:** `GET`

```
$ curl 'https://dev-api.unicro.co.kr:14147/api/v1/users/unicro123/status' -i -X GET \
    -H 'Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1'
```

**요청**

```
GET /api/v1/users/unicro123/status HTTP/1.1
Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1
Host: dev-api.unicro.co.kr:14147
```

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 132

{
  "result" : "SUCCESS",
  "msg" : "회원 등록 여부 조회 성공하였습니다.",
  "errorCd" : "",
  "data" : "NONE"
}
```

**Response Fields**

| 필드명     | 타입     | 설명                                                       |
| ------- | ------ | -------------------------------------------------------- |
| result  | String | 성공실패 여부 코드 (성공: SUCCESS, 실패: FAIL)                       |
| msg     | String | 응답 메시지                                                   |
| errorCd | String | 실패시 에러 코드                                                |
| data    | String | 유니크로 회원 상태(NONE:비회원, NORMAL:정상, SLEEP:휴면, WITHDRAWAL:탈퇴) |

#### 2.2 회원 탈퇴 <a href="#_2_2_-_" id="_2_2_-_"></a>

***

제휴사 회원 탈퇴 시 유니크로 회원 탈퇴를 위한 API입니다.

* **기능** 회원 탈퇴
* **URI** _/api/v1/users/{partnerUserId}/withdrawal_
* **Method:** `POST`

```
$ curl 'https://dev-api.unicro.co.kr:14147/api/v1/users/heesu/withdrawal' -i -X POST \
    -H 'Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1' \
    -H 'Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA'
```

**요청**

```
POST /api/v1/users/heesu/withdrawal HTTP/1.1
Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1
Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA
Host: dev-api.unicro.co.kr:14147
```

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 121

{
  "result" : "SUCCESS",
  "msg" : "회원 탈퇴 실패하였습니다.",
  "errorCd" : "VALID",
  "data" : null
}
```

**Response Fields**

| 필드명     | 타입     | 설명                                 |
| ------- | ------ | ---------------------------------- |
| result  | String | 성공실패 여부 코드 (성공: SUCCESS, 실패: FAIL) |
| msg     | String | 응답 메시지                             |
| errorCd | String | 실패시 에러 코드                          |
| data    | Null   |                                    |

### 3. 상품(판매자) <a href="#_3_" id="_3_"></a>

#### 3.1 상품 등록 <a href="#_3_1_-_" id="_3_1_-_"></a>

***

판매자가 상품등록을 위해 호출하는 API입니다.

* **기능** 상품 등록
* **URI** _/api/v1/items_
* **Method:** `POST`

```
$ curl 'https://dev-api.unicro.co.kr:14147/api/v1/items' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1' \
    -H 'Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA' \
    -H 'Accept: application/json' \
    -d '{
  "partnerItemNo" : "22090701",
  "itemName" : "상품명입니다",
  "itemPrice" : 3000,
  "selPayway" : [ "CARD", "BANK", "VIRTUAL_ACCOUNT", "VIRTUAL_ACCOUNT" ],
  "deliveryPayCd" : "CASH_ON_DELIVERY",
  "deliveryCd" : "PARTNER_DELIVERY",
  "imgUrl" : "https://dev-api.unicro.co.kr:14147/webasp_common/new_images/bi_unicro.gif",
  "mainCategoryCd" : "130",
  "subCategoryCd" : "150"
}'
```

**요청**

```
POST /api/v1/items HTTP/1.1
Content-Type: application/json
Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1
Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA
Accept: application/json
Content-Length: 399
Host: dev-api.unicro.co.kr:14147

{
  "partnerItemNo" : "22090701",
  "itemName" : "상품명입니다",
  "itemPrice" : 3000,
  "selPayway" : [ "CARD", "BANK", "VIRTUAL_ACCOUNT", "VIRTUAL_ACCOUNT" ],
  "deliveryPayCd" : "CASH_ON_DELIVERY",
  "deliveryCd" : "PARTNER_DELIVERY",
  "imgUrl" : "https://dev-api.unicro.co.kr:14147/webasp_common/new_images/bi_unicro.gif",
  "mainCategoryCd" : "130",
  "subCategoryCd" : "150"
}
```

**Request Fields**

| 필드명            | 타입     | 설명                                                              | 필수값  | 제한      |
| -------------- | ------ | --------------------------------------------------------------- | ---- | ------- |
| partnerItemNo  | String | 제휴사 상품고유식별번호                                                    | true |         |
| itemName       | String | 상품명                                                             | true | 200자 이하 |
| itemPrice      | Number | 상품가격                                                            | true | 3000 이상 |
| selPayway      | Array  | 결제가능한 결제수단 (CARD: 신용카드, BANK: 계좌이체, VIRTUAL\_ACCOUNT: 가상계좌 무통장) | true |         |
| deliveryPayCd  | String | 배송비부담 (CASH\_ON\_DELIVERY:착불(구매자부담), PRE\_PAYMENT:선불(판매자부담))    | true |         |
| deliveryCd     | String | 배송방법 (PARCEL\_DELIVERY:택배배송, PARTNER\_DELIVERY:제휴사배송)           | true |         |
| imgUrl         | String | 이미지 경로 URI                                                      |      |         |
| mainCategoryCd | String | 메인 카테고리 코드 (상품코드표 참고)                                           |      |         |
| subCategoryCd  | String | 서브 카테고리 코드 (상품코드표 참고)                                           |      |         |

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 304

{
  "result" : "SUCCESS",
  "msg" : "정상적으로 처리되었습니다.",
  "errorCd" : "",
  "data" : {
    "unicroItemNo" : "221000609451",
    "partnerItemNo" : "22090701",
    "statusCd" : "AVAILABLE_FOR_SALE",
    "itemName" : null,
    "itemPrice" : null,
    "divCode" : null
  }
}
```

**Response Fields**

| 필드명                | 타입     | 설명                                 |
| ------------------ | ------ | ---------------------------------- |
| result             | String | 성공실패 여부 코드 (성공: SUCCESS, 실패: FAIL) |
| msg                | String | 응답 메시지                             |
| errorCd            | String | 실패시 에러 코드                          |
| data.unicroItemNo  | String | 유니크로 상품고유식별번호                      |
| data.partnerItemNo | String | 제휴사 상품고유식별번호                       |
| data.statusCd      | String | 상품 상태                              |

### 4. 거래(제휴사) <a href="#_4_" id="_4_"></a>

#### 4.1 제휴사 거래번호로 거래 조회 <a href="#_4_1_-_-_-_" id="_4_1_-_-_-_"></a>

***

제휴사 거래번호로 거래를 조회하는 API입니다.

* **기능** 제휴사 거래번호로 거래 조회
* **URI** _/api/v1/trades/partner/{partnerTradeNo}_
* **Method:** `GET`

```
$ curl 'https://dev-api.unicro.co.kr:14147/api/v1/trades/partner/2022045465' -i -X GET \
    -H 'Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1' \
    -H 'Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA'
```

**요청**

```
GET /api/v1/trades/partner/2022045465 HTTP/1.1
Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1
Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA
Host: dev-api.unicro.co.kr:14147
```

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 230

{
  "result" : "SUCCESS",
  "msg" : "정상적으로 처리되었습니다.",
  "errorCd" : "",
  "data" : {
    "unicroTradeNo" : "202209011231",
    "partnerTradeNo" : "2022045465",
    "statusCd" : "PAY_APPROVED"
  }
}
```

**Response Fields**

| 필드명                 | 타입     | 설명                                 |
| ------------------- | ------ | ---------------------------------- |
| result              | String | 성공실패 여부 코드 (성공: SUCCESS, 실패: FAIL) |
| msg                 | String | 응답 메시지                             |
| errorCd             | String | 실패시 에러 코드                          |
| data.unicroTradeNo  | String | 유니크로 거래고유식별번호                      |
| data.partnerTradeNo | String | 제휴사 거래고유식별번호                       |
| data.statusCd       | String | 거래 상태                              |

#### 4.2 유니크로 거래번호로 거래 조회 <a href="#_4_2_-_-_-_" id="_4_2_-_-_-_"></a>

***

유니크로 거래번호로 거래를 조회하는 API입니다.

* **기능** 유니크로 거래번호로 거래 조회
* **URI** _/api/v1/trades/{unicroTradeNo}_
* **Method:** `GET`

```
$ curl 'https://dev-api.unicro.co.kr:14147/api/v1/trades/202204546555' -i -X GET \
    -H 'Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1' \
    -H 'Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA'
```

**요청**

```
GET /api/v1/trades/202204546555 HTTP/1.1
Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1
Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA
Host: dev-api.unicro.co.kr:14147
```

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 232

{
  "result" : "SUCCESS",
  "msg" : "정상적으로 처리되었습니다.",
  "errorCd" : "",
  "data" : {
    "unicroTradeNo" : "202204546555",
    "partnerTradeNo" : "202209011241",
    "statusCd" : "PAY_APPROVED"
  }
}
```

**Response Fields**

| 필드명                 | 타입     | 설명                                 |
| ------------------- | ------ | ---------------------------------- |
| result              | String | 성공실패 여부 코드 (성공: SUCCESS, 실패: FAIL) |
| msg                 | String | 응답 메시지                             |
| errorCd             | String | 실패시 에러 코드                          |
| data.unicroTradeNo  | String | 유니크로 거래고유식별번호                      |
| data.partnerTradeNo | String | 제휴사 거래고유식별번호                       |
| data.statusCd       | String | 거래 상태                              |

#### 4.3 수동 배송완료 처리 (제휴사 관리자) <a href="#_4_3_-_-_-_-_" id="_4_3_-_-_-_-_"></a>

***

제휴사 관리자가 수동으로 배송완료 처리하는 API입니다.\
수동 배송완료 처리시 배송에 대한 책임은 제휴사에 있습니다.

**배송완료 처리가 가능한 거래상태**

| 상태            | 설명                       |
| ------------- | ------------------------ |
| PAY\_APPROVED | 요청 후 DELIVERY\_DONE로 변경됨 |
| DELIVERY\_ING | 요청 후 DELIVERY\_DONE로 변경됨 |

* **기능** 제휴사 관리자 배송완료 처리
* **URI** _/api/v1/trades/{unicroTradeNo}/delivery/done_
* **Method:** `POST`

```
$ curl 'https://dev-api.unicro.co.kr:14147/api/v1/trades/202209050000/delivery/done' -i -X POST \
    -H 'Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1' \
    -H 'Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA'
```

**요청**

```
POST /api/v1/trades/202209050000/delivery/done HTTP/1.1
Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1
Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA
Host: dev-api.unicro.co.kr:14147
```

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 230

{
  "result" : "SUCCESS",
  "msg" : "배송완료 처리되었습니다.",
  "errorCd" : "",
  "data" : {
    "unicroTradeNo" : "202209050000",
    "partnerTradeNo" : "202209011241",
    "statusCd" : "DELIVERY_DONE"
  }
}
```

**Response Fields**

| 필드명                 | 타입     | 설명                                 |
| ------------------- | ------ | ---------------------------------- |
| result              | String | 성공실패 여부 코드 (성공: SUCCESS, 실패: FAIL) |
| msg                 | String | 응답 메시지                             |
| errorCd             | String | 실패시 에러 코드                          |
| data.unicroTradeNo  | String | 유니크로 거래고유식별번호                      |
| data.partnerTradeNo | String | 제휴사 거래고유식별번호                       |
| data.statusCd       | String | 거래 상태                              |

### 5. 거래(구매자) <a href="#_5_" id="_5_"></a>

#### 5.1 구매자 결제 취소 <a href="#_5_1_-_-_" id="_5_1_-_-_"></a>

***

구매자가 결제 취소를 요청하는 API입니다.

**구매자 결제 취소가 가능한 거래상태**

| 상태            | 설명                                                       |
| ------------- | -------------------------------------------------------- |
| PAY\_STANDBY  | 요청 후 CANCEL\_DONE\_BUYER로 변경됨                            |
| PAY\_APPROVED | 요청 후 CANCEL\_REQ로 변경됨 (판매자가 취소요청을 승인하여야 거래취소 되는 상태로 변경됨) |

* **기능** 구매 취소 요청
* **URI** _/api/v1/buyer/trades/{unicroTradeNo}/cancel_
* **Method:** `POST`

```
$ curl 'https://dev-api.unicro.co.kr:14147/api/v1/buyer/trades/202209051745/cancel' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1' \
    -H 'Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA' \
    -H 'Accept: application/json' \
    -d '{
  "cancelCd" : "",
  "cancelMemo" : "테스트용"
}'
```

**요청**

```
POST /api/v1/buyer/trades/202209051745/cancel HTTP/1.1
Content-Type: application/json
Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1
Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA
Accept: application/json
Content-Length: 57
Host: dev-api.unicro.co.kr:14147

{
  "cancelCd" : "",
  "cancelMemo" : "테스트용"
}
```

**Request Fields**

| 필드명        | 타입     | 설명          | 필수값  | 제한 |
| ---------- | ------ | ----------- | ---- | -- |
| cancelCd   | String | 취소 사유코드     | true |    |
| cancelMemo | String | 취소 사유(직접입력) |      |    |

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 224

{
  "result" : "SUCCESS",
  "msg" : "구매 취소 되었습니다.",
  "errorCd" : "",
  "data" : {
    "unicroTradeNo" : "202209051745",
    "partnerTradeNo" : "1224545",
    "statusCd" : "CANCEL_DONE_BUYER"
  }
}
```

**Response Fields**

| 필드명                 | 타입     | 설명                                 |
| ------------------- | ------ | ---------------------------------- |
| result              | String | 성공실패 여부 코드 (성공: SUCCESS, 실패: FAIL) |
| msg                 | String | 응답 메시지                             |
| errorCd             | String | 실패시 에러 코드                          |
| data.unicroTradeNo  | String | 유니크로 거래고유식별번호                      |
| data.partnerTradeNo | String | 제휴사 거래고유식별번호                       |
| data.statusCd       | String | 거래 상태                              |

#### 5.2 구매자 반품 요청 <a href="#_5_2_-_-_" id="_5_2_-_-_"></a>

***

구매자가 배송중인 거래를 반품요청하는 API입니다.

**구매자 반품요청이 가능한 거래상태**

| 상태            | 설명                    |
| ------------- | --------------------- |
| DELIVERY\_ING | 요청 후 RETURN\_REQ로 변경됨 |

* **기능** 구매자 반품 요청
* **URI** _/api/v1/buyer/trades/{unicroTradeNo}/return/create_
* **Method:** `POST`

```
$ curl 'https://dev-api.unicro.co.kr:14147/api/v1/buyer/trades/202209051745/return/create' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1' \
    -H 'Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA' \
    -H 'Accept: application/json' \
    -d '{
  "returnDeliveryPayCd" : "CASH_ON_DELIVERY",
  "returnCd" : "",
  "returnMemo" : ""
}'
```

**요청**

```
POST /api/v1/buyer/trades/202209051745/return/create HTTP/1.1
Content-Type: application/json
Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1
Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA
Accept: application/json
Content-Length: 92
Host: dev-api.unicro.co.kr:14147

{
  "returnDeliveryPayCd" : "CASH_ON_DELIVERY",
  "returnCd" : "",
  "returnMemo" : ""
}
```

**Request Fields**

| 필드명                 | 타입     | 설명                                                 | 필수값  | 제한 |
| ------------------- | ------ | -------------------------------------------------- | ---- | -- |
| returnDeliveryPayCd | String | 반품 배송비 부담 (CASH\_ON\_DELIVERY:착불, PRE\_PAYMENT:선불) | true |    |
| returnCd            | String | 반품 사유코드                                            | true |    |
| returnMemo          | String | 반품 사유(직접입력)                                        |      |    |

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 226

{
  "result" : "SUCCESS",
  "msg" : "반품요청이 완료 되었습니다.",
  "errorCd" : "",
  "data" : {
    "unicroTradeNo" : "202209051745",
    "partnerTradeNo" : "1224545",
    "statusCd" : "CANCEL_REQ"
  }
}
```

**Response Fields**

| 필드명                 | 타입     | 설명                                 |
| ------------------- | ------ | ---------------------------------- |
| result              | String | 성공실패 여부 코드 (성공: SUCCESS, 실패: FAIL) |
| msg                 | String | 응답 메시지                             |
| errorCd             | String | 실패시 에러 코드                          |
| data.unicroTradeNo  | String | 유니크로 거래고유식별번호                      |
| data.partnerTradeNo | String | 제휴사 거래고유식별번호                       |
| data.statusCd       | String | 거래 상태                              |

#### 5.3 구매자 반품 배송정보 기입 <a href="#_5_3_-_-_-_" id="_5_3_-_-_-_"></a>

***

구매자가 배송중인 거래를 반품요청하는 API입니다.

**구매자 반품 배송정보 기입이 가능한 거래상태**

| 상태          | 설명                    |
| ----------- | --------------------- |
| RETURN\_AGR | 요청 후 RETURN\_ING로 변경됨 |

* **기능** 구매자 반품 배송정보 기입
* **URI** _/api/v1/buyer/trades/{unicroTradeNo}/return/delivery_
* **Method:** `POST`

```
$ curl 'https://dev-api.unicro.co.kr:14147/api/v1/buyer/trades/202209051745/return/delivery' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1' \
    -H 'Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA' \
    -H 'Accept: application/json' \
    -d '{
  "deliveryCompCd" : "004",
  "invoiceNo" : "6044000000000"
}'
```

**요청**

```
POST /api/v1/buyer/trades/202209051745/return/delivery HTTP/1.1
Content-Type: application/json
Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1
Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA
Accept: application/json
Content-Length: 66
Host: dev-api.unicro.co.kr:14147

{
  "deliveryCompCd" : "004",
  "invoiceNo" : "6044000000000"
}
```

**Request Fields**

| 필드명                  | 타입     | 설명                   | 필수값  | 제한 |
| -------------------- | ------ | -------------------- | ---- | -- |
| deliveryCompCd       | String | 택배사 코드 (유니크로 코드표 참고) | true |    |
| invoiceNo            | String | 송장번호                 | true |    |
| returnSenderName     | String | 구매자명                 |      |    |
| returnSenderHhpNo    | String | 구매자 연락처              |      |    |
| returnSenderZip      | String | 구매자 우편번호             |      |    |
| returnSenderAddress1 | String | 구매자 주소               |      |    |
| returnSenderAddress2 | String | 구매자 상세주소             |      |    |

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 240

{
  "result" : "SUCCESS",
  "msg" : "반품 배송정보 기입이 완료 되었습니다.",
  "errorCd" : "",
  "data" : {
    "unicroTradeNo" : "202209051745",
    "partnerTradeNo" : "1224545",
    "statusCd" : "RETURN_ING"
  }
}
```

**Response Fields**

| 필드명                 | 타입     | 설명                                 |
| ------------------- | ------ | ---------------------------------- |
| result              | String | 성공실패 여부 코드 (성공: SUCCESS, 실패: FAIL) |
| msg                 | String | 응답 메시지                             |
| errorCd             | String | 실패시 에러 코드                          |
| data.unicroTradeNo  | String | 유니크로 거래고유식별번호                      |
| data.partnerTradeNo | String | 제휴사 거래고유식별번호                       |
| data.statusCd       | String | 거래 상태                              |

#### 5.4 거래 완료 <a href="#_5_4_-_" id="_5_4_-_"></a>

***

구매자가 상품을 받고 거래 완료처리하는 API입니다.

**거래 완료가 가능한 거래상태**

| 상태             | 설명                   |
| -------------- | -------------------- |
| DELIVERY\_ING  | 요청 후 PAY\_DONE으로 변경됨 |
| DELIVERY\_DONE | 요청 후 PAY\_DONE으로 변경됨 |

* **기능** 거래 완료
* **URI** _/api/v1/buyer/trades/{unicroTradeNo}/done_
* **Method:** `POST`

```
$ curl 'https://dev-api.unicro.co.kr:14147/api/v1/buyer/trades/202209051745/done' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1' \
    -H 'Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA' \
    -H 'Accept: application/json'
```

**요청**

```
POST /api/v1/buyer/trades/202209051745/done HTTP/1.1
Content-Type: application/json
Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1
Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA
Accept: application/json
Host: dev-api.unicro.co.kr:14147
```

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 218

{
  "result" : "SUCCESS",
  "msg" : "거래가 완료 되었습니다.",
  "errorCd" : "",
  "data" : {
    "unicroTradeNo" : "202209051745",
    "partnerTradeNo" : "1224545",
    "statusCd" : "PAY_DONE"
  }
}
```

**Response Fields**

| 필드명                 | 타입     | 설명                                 |
| ------------------- | ------ | ---------------------------------- |
| result              | String | 성공실패 여부 코드 (성공: SUCCESS, 실패: FAIL) |
| msg                 | String | 응답 메시지                             |
| errorCd             | String | 실패시 에러 코드                          |
| data.unicroTradeNo  | String | 유니크로 거래고유식별번호                      |
| data.partnerTradeNo | String | 제휴사 거래고유식별번호                       |
| data.statusCd       | String | 거래 상태                              |

#### 5.5 구매자 거래 상세 조회 <a href="#_5_5_-_-_-_" id="_5_5_-_-_-_"></a>

***

구매자가 거래 정보를 조회하는 API입니다.

* **기능** 구매자 거래 상세 조회
* **URI** _/api/v1/buyer/trades/{unicroTradeNo}_
* **Method:** `GET`

```
$ curl 'https://dev-api.unicro.co.kr:14147/api/v1/buyer/trades/202209050000' -i -X GET \
    -H 'Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1' \
    -H 'Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA'
```

**요청**

```
GET /api/v1/buyer/trades/202209050000 HTTP/1.1
Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1
Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA
Host: dev-api.unicro.co.kr:14147
```

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 623

{
  "result" : "SUCCESS",
  "msg" : "구매자 거래 조회에 성공했습니다.",
  "errorCd" : "",
  "data" : {
    "unicroTradeNo" : "202209050000",
    "partnerTradeNo" : "123456789",
    "payway" : "VIRTUAL_ACCOUNT",
    "buyAmt" : 3000,
    "tradeDate" : "2022-11-04T15:31:43.7779158",
    "statusCd" : "SETTLEMENT_DONE",
    "deliveryCompCd" : "",
    "invoiceNo" : "",
    "unicroItemNo" : "20220091300000",
    "partnerItemNo" : "2022009130000A0",
    "bankName" : "신한은행",
    "accountNo" : "10000000000",
    "accountName" : "유니크로",
    "vaDueDate" : "202209150100000"
  }
}
```

**Response Fields**

| 필드명                 | 타입     | 설명                                 |
| ------------------- | ------ | ---------------------------------- |
| result              | String | 성공실패 여부 코드 (성공: SUCCESS, 실패: FAIL) |
| msg                 | String | 응답 메시지                             |
| errorCd             | String | 실패시 에러 코드                          |
| data.unicroTradeNo  | String | 유니크로 거래고유식별번호                      |
| data.partnerTradeNo | String | 제휴사 거래고유식별번호                       |
| data.payway         | String | 결제수단                               |
| data.buyAmt         | Number | 결제금액                               |
| data.tradeDate      | String | 결제 일시                              |
| data.statusCd       | String | 거래 상태                              |
| data.deliveryCompCd | String | 택배사 코드                             |
| data.invoiceNo      | String | 송장번호                               |
| data.unicroItemNo   | String | 유니크로 상품고유식별번호                      |
| data.partnerItemNo  | String | 제휴사 상품고유식별번호                       |
| data.statusCd       | String | 거래 상태                              |
| data.bankName       | String | 입금정보-은행                            |
| data.accountNo      | String | 입금정보-계좌번호                          |
| data.accountName    | String | 예금주                                |
| data.vaDueDate      | String | 무통장입금기한                            |

#### 5.6 주소 정보 기입 <a href="#_5_6_-_-_" id="_5_6_-_-_"></a>

***

구매자가 주소 정보를 기입하는 API입니다.

* **기능** 주소 정보 기입
* **URI** _/api/v1/buyer/trades/{unicroTradeNo}/address_
* **Method:** `POST`

```
$ curl 'https://dev-api.unicro.co.kr:14147/api/v1/buyer/trades/202209050000/address' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1' \
    -H 'Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA' \
    -H 'Accept: application/json' \
    -d '{
  "buyerZip" : "16878",
  "buyerAddress1" : "경기 용인시 수지구 디지털벨리로 81 (죽전동, 다우기술)",
  "buyerAddress2" : "6층 플랫폼개발팀"
}'
```

**요청**

```
POST /api/v1/buyer/trades/202209050000/address HTTP/1.1
Content-Type: application/json
Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1
Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA
Accept: application/json
Content-Length: 175
Host: dev-api.unicro.co.kr:14147

{
  "buyerZip" : "16878",
  "buyerAddress1" : "경기 용인시 수지구 디지털벨리로 81 (죽전동, 다우기술)",
  "buyerAddress2" : "6층 플랫폼개발팀"
}
```

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 237

{
  "result" : "SUCCESS",
  "msg" : "주소정보 기입이 완료 되었습니다.",
  "errorCd" : "",
  "data" : {
    "unicroTradeNo" : "202209050000",
    "partnerTradeNo" : "123456789",
    "statusCd" : "PAY_APPROVED"
  }
}
```

**Response Fields**

| 필드명                 | 타입     | 설명                                 |
| ------------------- | ------ | ---------------------------------- |
| result              | String | 성공실패 여부 코드 (성공: SUCCESS, 실패: FAIL) |
| msg                 | String | 응답 메시지                             |
| errorCd             | String | 실패시 에러 코드                          |
| data.unicroTradeNo  | String | 유니크로 거래고유식별번호                      |
| data.partnerTradeNo | String | 제휴사 거래고유식별번호                       |
| data.statusCd       | String | 거래 상태                              |

### 6. 거래(판매자) <a href="#_6_" id="_6_"></a>

#### 6.1 판매자 결제취소 동의 <a href="#_6_1_-_-_" id="_6_1_-_-_"></a>

***

판매자가 구매자 결제취소 요청에 동의하는 API입니다.

**판매자 결제취소 동의가 가능한 거래상태**

| 상태          | 설명                            |
| ----------- | ----------------------------- |
| CANCEL\_REQ | 요청 후 CANCEL\_DONE\_BUYER로 변경됨 |

* **기능** 판매자 결제취소 동의
* **URI** _/api/v1/seller/trades/{unicroTradeNo}/cancel/agree_
* **Method:** `POST`

```
$ curl 'https://dev-api.unicro.co.kr:14147/api/v1/seller/trades/202209050000/cancel/agree' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1' \
    -H 'Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA' \
    -H 'Accept: application/json'
```

**요청**

```
POST /api/v1/seller/trades/202209050000/cancel/agree HTTP/1.1
Content-Type: application/json
Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1
Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA
Accept: application/json
Host: dev-api.unicro.co.kr:14147
```

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 255

{
  "result" : "SUCCESS",
  "msg" : "구매자 결제취소에 동의가 완료 되었습니다.",
  "errorCd" : "",
  "data" : {
    "unicroTradeNo" : "202209050000",
    "partnerTradeNo" : "123456789",
    "statusCd" : "CANCEL_DONE_BUYER"
  }
}
```

**Response Fields**

| 필드명                 | 타입     | 설명                                 |
| ------------------- | ------ | ---------------------------------- |
| result              | String | 성공실패 여부 코드 (성공: SUCCESS, 실패: FAIL) |
| msg                 | String | 응답 메시지                             |
| errorCd             | String | 실패시 에러 코드                          |
| data.unicroTradeNo  | String | 유니크로 거래고유식별번호                      |
| data.partnerTradeNo | String | 제휴사 거래고유식별번호                       |
| data.statusCd       | String | 거래 상태                              |

#### 6.2 판매자 거래취소 <a href="#_6_2_-_" id="_6_2_-_"></a>

***

판매자가 거래를 취소하는 API입니다.

**판매자 거래 취소가 가능한 거래상태**

| 상태            | 설명                             |
| ------------- | ------------------------------ |
| PAY\_APPROVED | 요청 후 CANCEL\_DONE\_SELLER로 변경됨 |

* **기능** 판매자 거래 취소
* **URI** _/api/v1/seller/trades/{unicroTradeNo}/cancel/done_
* **Method:** `POST`

```
$ curl 'https://dev-api.unicro.co.kr:14147/api/v1/seller/trades/202209050000/cancel/done' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1' \
    -H 'Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA' \
    -H 'Accept: application/json' \
    -d '{
  "cancelCd" : "39",
  "cancelMemo" : "판매취소사유(직접입력)"
}'
```

**요청**

```
POST /api/v1/seller/trades/202209050000/cancel/done HTTP/1.1
Content-Type: application/json
Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1
Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA
Accept: application/json
Content-Length: 79
Host: dev-api.unicro.co.kr:14147

{
  "cancelCd" : "39",
  "cancelMemo" : "판매취소사유(직접입력)"
}
```

**Request Fields**

| 필드명        | 타입     | 설명            | 필수값  | 제한      |
| ---------- | ------ | ------------- | ---- | ------- |
| cancelCd   | String | 판매취소 사유코드     | true |         |
| cancelMemo | String | 판매취소 사유(직접입력) |      | 500자 이내 |

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 247

{
  "result" : "SUCCESS",
  "msg" : "판매자 거래 취소가 완료 되었습니다.",
  "errorCd" : "",
  "data" : {
    "unicroTradeNo" : "202209050000",
    "partnerTradeNo" : "123456789",
    "statusCd" : "CANCEL_DONE_SELLER"
  }
}
```

**Response Fields**

| 필드명                 | 타입     | 설명                                 |
| ------------------- | ------ | ---------------------------------- |
| result              | String | 성공실패 여부 코드 (성공: SUCCESS, 실패: FAIL) |
| msg                 | String | 응답 메시지                             |
| errorCd             | String | 실패시 에러 코드                          |
| data.unicroTradeNo  | String | 유니크로 거래고유식별번호                      |
| data.partnerTradeNo | String | 제휴사 거래고유식별번호                       |
| data.statusCd       | String | 거래 상태                              |

#### 6.3 배송정보 기입 <a href="#_6_3_-_" id="_6_3_-_"></a>

***

판매자가 배송정보를 기입하는 API입니다.

**판매자 배송정보 기입이 가능한 거래상태**

| 상태            | 설명                      |
| ------------- | ----------------------- |
| PAY\_APPROVED | 요청 후 DELIVERY\_ING로 변경됨 |

* **기능** 판매자 배송정보 기입
* **URI** _/api/v1/seller/trades/{unicroTradeNo}/delivery_
* **Method:** `POST`

```
$ curl 'https://dev-api.unicro.co.kr:14147/api/v1/seller/trades/202209050000/delivery' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1' \
    -H 'Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA' \
    -H 'Accept: application/json' \
    -d '{
  "tradeNo" : null,
  "deliveryPayCd" : "PRE_PAYMENT",
  "deliveryCompCd" : "005",
  "invoiceNo" : "1234567890",
  "senderName" : "권희수",
  "senderHhpNo" : "010-9939-2814",
  "senderZip" : "16878",
  "senderAddress1" : "경기 용인시 수지구 디지털벨리로 81 (죽전동, 다우기술)",
  "senderAddress2" : "6층 플랫폼개발팀"
}'
```

**요청**

```
POST /api/v1/seller/trades/202209050000/delivery HTTP/1.1
Content-Type: application/json
Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1
Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA
Accept: application/json
Content-Length: 362
Host: dev-api.unicro.co.kr:14147

{
  "tradeNo" : null,
  "deliveryPayCd" : "PRE_PAYMENT",
  "deliveryCompCd" : "005",
  "invoiceNo" : "1234567890",
  "senderName" : "권희수",
  "senderHhpNo" : "010-9939-2814",
  "senderZip" : "16878",
  "senderAddress1" : "경기 용인시 수지구 디지털벨리로 81 (죽전동, 다우기술)",
  "senderAddress2" : "6층 플랫폼개발팀"
}
```

**Request Fields**

| 필드명            | 타입     | 설명                                              | 필수값  | 제한 |
| -------------- | ------ | ----------------------------------------------- | ---- | -- |
| deliveryPayCd  | String | 판매자 택배 (CASH\_ON\_DELIVERY:착불, PRE\_PAYMENT:선불) | true |    |
| deliveryCompCd | String | 택배사 코드 (유니크로 코드표 참고)                            | true |    |
| invoiceNo      | String | 송장번호                                            | true |    |
| senderName     | String | 판매자명                                            |      |    |
| senderHhpNo    | String | 판매자 연락처                                         |      |    |
| senderZip      | String | 판매자 우편번호                                        |      |    |
| senderAddress1 | String | 판매자 주소                                          |      |    |
| senderAddress2 | String | 판매자 상세주소                                        |      |    |

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 237

{
  "result" : "SUCCESS",
  "msg" : "배송정보 기입이 완료 되었습니다.",
  "errorCd" : "",
  "data" : {
    "unicroTradeNo" : "202209050000",
    "partnerTradeNo" : "123456789",
    "statusCd" : "DELIVERY_ING"
  }
}
```

**Response Fields**

| 필드명                 | 타입     | 설명                                 |
| ------------------- | ------ | ---------------------------------- |
| result              | String | 성공실패 여부 코드 (성공: SUCCESS, 실패: FAIL) |
| msg                 | String | 응답 메시지                             |
| errorCd             | String | 실패시 에러 코드                          |
| data.unicroTradeNo  | String | 유니크로 거래고유식별번호                      |
| data.partnerTradeNo | String | 제휴사 거래고유식별번호                       |
| data.statusCd       | String | 거래 상태                              |

#### 6.4 반품 수락 <a href="#_6_4_-_" id="_6_4_-_"></a>

***

판매자가 구매자의 반품 요청을 수락하는 API입니다.

**반품 수락이 가능한 거래상태**

| 상태          | 설명                    |
| ----------- | --------------------- |
| RETURN\_REQ | 요청 후 RETURN\_AGR로 변경됨 |

* **기능** 반품 수락
* **URI** _/api/v1/seller/trades/{unicroTradeNo}/return/agree_
* **Method:** `POST`

```
$ curl 'https://dev-api.unicro.co.kr:14147/api/v1/seller/trades/202209050000/return/agree' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1' \
    -H 'Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA' \
    -H 'Accept: application/json' \
    -d '{
  "senderName" : "권희수",
  "senderZip" : "16878",
  "senderAddress1" : "경기 용인시 수지구 디지털벨리로 81 (죽전동, 다우기술)",
  "senderAddress2" : "6층 플랫폼개발팀",
  "senderHhpNo" : "010-9939-2814"
}'
```

**요청**

```
POST /api/v1/seller/trades/202209050000/return/agree HTTP/1.1
Content-Type: application/json
Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1
Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA
Accept: application/json
Content-Length: 245
Host: dev-api.unicro.co.kr:14147

{
  "senderName" : "권희수",
  "senderZip" : "16878",
  "senderAddress1" : "경기 용인시 수지구 디지털벨리로 81 (죽전동, 다우기술)",
  "senderAddress2" : "6층 플랫폼개발팀",
  "senderHhpNo" : "010-9939-2814"
}
```

**Request Fields**

| 필드명            | 타입     | 설명       | 필수값  | 제한 |
| -------------- | ------ | -------- | ---- | -- |
| senderName     | String | 판매자명     | true |    |
| senderHhpNo    | String | 판매자 연락처  | true |    |
| senderZip      | String | 판매자 우편번호 | true |    |
| senderAddress1 | String | 판매자 주소   | true |    |
| senderAddress2 | String | 판매자 상세주소 | true |    |

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 228

{
  "result" : "SUCCESS",
  "msg" : "반품 요청을 수락하였습니다.",
  "errorCd" : "",
  "data" : {
    "unicroTradeNo" : "202209050000",
    "partnerTradeNo" : "123456789",
    "statusCd" : "RETURN_AGR"
  }
}
```

**Response Fields**

| 필드명                 | 타입     | 설명                                 |
| ------------------- | ------ | ---------------------------------- |
| result              | String | 성공실패 여부 코드 (성공: SUCCESS, 실패: FAIL) |
| msg                 | String | 응답 메시지                             |
| errorCd             | String | 실패시 에러 코드                          |
| data.unicroTradeNo  | String | 유니크로 거래고유식별번호                      |
| data.partnerTradeNo | String | 제휴사 거래고유식별번호                       |
| data.statusCd       | String | 거래 상태                              |

#### 6.5 반품 완료 <a href="#_6_5_-_" id="_6_5_-_"></a>

***

판매자가 반품 완료하는 API입니다.

**반품 완료가 가능한 거래상태**

| 상태          | 설명                     |
| ----------- | ---------------------- |
| RETURN\_ING | 요청 후 RETURN\_DONE로 변경됨 |

* **기능** 반품 완료
* **URI** _/api/v1/seller/trades/{unicroTradeNo}/return/done_
* **Method:** `POST`

```
$ curl 'https://dev-api.unicro.co.kr:14147/api/v1/seller/trades/202209050000/return/done' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1' \
    -H 'Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA' \
    -H 'Accept: application/json'
```

**요청**

```
POST /api/v1/seller/trades/202209050000/return/done HTTP/1.1
Content-Type: application/json
Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1
Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA
Accept: application/json
Host: dev-api.unicro.co.kr:14147
```

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 225

{
  "result" : "SUCCESS",
  "msg" : "반품완료 처리되었습니다.",
  "errorCd" : "",
  "data" : {
    "unicroTradeNo" : "202209050000",
    "partnerTradeNo" : "123456789",
    "statusCd" : "RETURN_DONE"
  }
}
```

**Response Fields**

| 필드명                 | 타입     | 설명                                 |
| ------------------- | ------ | ---------------------------------- |
| result              | String | 성공실패 여부 코드 (성공: SUCCESS, 실패: FAIL) |
| msg                 | String | 응답 메시지                             |
| errorCd             | String | 실패시 에러 코드                          |
| data.unicroTradeNo  | String | 유니크로 거래고유식별번호                      |
| data.partnerTradeNo | String | 제휴사 거래고유식별번호                       |
| data.statusCd       | String | 거래 상태                              |

#### 6.6 판매자 거래 상세 조회 <a href="#_6_6_-_-_-_" id="_6_6_-_-_-_"></a>

***

판매자가 거래 정보를 조회하는 API입니다.

* **기능** 판매자 거래 상세 조회
* **URI** _/api/v1/seller/trades/{unicroTradeNo}_
* **Method:** `GET`

```
$ curl 'https://dev-api.unicro.co.kr:14147/api/v1/seller/trades/202209050000' -i -X GET \
    -H 'Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1' \
    -H 'Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA'
```

**요청**

```
GET /api/v1/seller/trades/202209050000 HTTP/1.1
Partner-Api-Key: 80ADFEB2B6F39CCB06B645387B581AE6C4D8CDDCA68CAE8E815B17DE642B3AD1
Unicro_User_Token: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzNTgzOTkiLCJhdXRoIjoiUk9MRV9VU0VSIiwiZXhwIjoxNjY1MTM3MDYxfQ.o0XDRqP1v4zUaOIkPLU_wIKqK9sA4SLhtGHvr68r0MWbg1iP-LH0fPb8yvXFpQNTOzG4ED2tt5h69T_6KnvOrA
Host: dev-api.unicro.co.kr:14147
```

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 497

{
  "result" : "SUCCESS",
  "msg" : "판매자 거래 조회에 성공했습니다.",
  "errorCd" : "",
  "data" : {
    "unicroTradeNo" : "202209050000",
    "partnerTradeNo" : "123456789",
    "payway" : "CARD",
    "buyAmt" : 3000,
    "sellerAmt" : 2500,
    "tradeDate" : "2022-11-04T15:31:44.440445",
    "statusCd" : "SETTLEMENT_DONE",
    "deliveryCompCd" : "005",
    "invoiceNo" : "1234567890",
    "unicroItemNo" : "220900609127",
    "partnerItemNo" : "22090611"
  }
}
```

**Response Fields**

| 필드명                 | 타입     | 설명                                 |
| ------------------- | ------ | ---------------------------------- |
| result              | String | 성공실패 여부 코드 (성공: SUCCESS, 실패: FAIL) |
| msg                 | String | 응답 메시지                             |
| errorCd             | String | 실패시 에러 코드                          |
| data.unicroTradeNo  | String | 유니크로 거래고유식별번호                      |
| data.partnerTradeNo | String | 제휴사 거래고유식별번호                       |
| data.payway         | String | 결제수단                               |
| data.buyAmt         | Number | 결제금액                               |
| data.sellerAmt      | Number | 판매자 정산금액                           |
| data.tradeDate      | String | 결제 일시                              |
| data.statusCd       | String | 거래 상태                              |
| data.deliveryCompCd | String | 택배사 코드                             |
| data.invoiceNo      | String | 송장번호                               |
| data.unicroItemNo   | String | 유니크로 상품고유식별번호                      |
| data.partnerItemNo  | String | 제휴사 상품고유식별번호                       |
