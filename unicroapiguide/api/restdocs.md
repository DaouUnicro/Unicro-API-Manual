# 제휴사 API

### 1. 인증 <a href="#_1_" id="_1_"></a>

**1.1 사용자 인증 토큰 발급**

***

API 호출시 헤더에 필수값인 사용자 인증 토큰 발급을 위해 사용하는 API입니다.

* **기능** 사용자 인증 토큰 발급
* **URI** /api/v1/auth
* **Method:** `POST`

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/auth' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -d '{
  "unicroPartnerKey" : "SDKFSPEFMSDLFSOEF",
  "partnerUserId" : "heesu@daou.co.kr"
}'
```

**요청**

```
POST /api/v1/auth HTTP/1.1
Content-Type: application/json
Accept: application/json
Content-Length: 89
Host: stg-api.unicro.co.kr:14147

{
  "unicroPartnerKey" : "SDKFSPEFMSDLFSOEF",
  "partnerUserId" : "heesu@daou.co.kr"
}
```

**Request Fields**

| 필드명              | 타입     | 설명           | 필수값  | 제한 |
| ---------------- | ------ | ------------ | ---- | -- |
| unicroPartnerKey | String | 유니크로 제휴사 발급키 | true |    |
| partnerUserId    | String | 제휴사 사용자 아이디  | true |    |

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 163

{
  "result" : "SUCCESS",
  "msg" : "토큰 발급을 성공했습니다.",
  "errorCd" : "",
  "data" : {
    "unicroUserKey" : "DQKDFMSEISFMDKSFOES"
  }
}
```

**Response Fields**

| 필드명                | 타입     | 설명                                 |
| ------------------ | ------ | ---------------------------------- |
| result             | String | 성공실패 여부 코드 (성공: SUCCESS, 실패: FAIL) |
| msg                | String | 응답 메시지                             |
| errorCd            | String | 실패시 에러 코드                          |
| data.unicroUserKey | String | 유니크로 사용자 식별키(인증 토큰)                |

### 2. 상품(판매자) <a href="#_2_" id="_2_"></a>

**2.1 상품 등록**

***

판매자가 상품등록을 위해 호출하는 API입니다.

* **기능** 상품 등록
* **URI** /api/v1/items
* **Method:** `POST`

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/items' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -d '{
  "sellerUnicroUserKey" : "UDdSfN5d525sD5FSD51",
  "partnerItemNo" : "22090701",
  "itemName" : "상품명입니다",
  "itemPrice" : 3000,
  "selPayway" : [ "CARD", "BANK", "VIRTUAL_ACCOUNT" ],
  "deliveryPayCd" : "CASH_ON_DELIVERY",
  "imgUrl" : "https://stg-api.unicro.co.kr:14147/webasp_common/new_images/bi_unicro.gif",
  "mainCategoryCd" : "010",
  "subCategoryCd" : "010"
}'
```

**요청**

```
POST /api/v1/items HTTP/1.1
Content-Type: application/json
Accept: application/json
Content-Length: 392
Host: stg-api.unicro.co.kr:14147

{
  "sellerUnicroUserKey" : "UDdSfN5d525sD5FSD51",
  "partnerItemNo" : "22090701",
  "itemName" : "상품명입니다",
  "itemPrice" : 3000,
  "selPayway" : [ "CARD", "BANK", "VIRTUAL_ACCOUNT" ],
  "deliveryPayCd" : "CASH_ON_DELIVERY",
  "imgUrl" : "https://stg-api.unicro.co.kr:14147/webasp_common/new_images/bi_unicro.gif",
  "mainCategoryCd" : "010",
  "subCategoryCd" : "010"
}
```

**Request Fields**

| 필드명                 | 타입     | 설명                                                              | 필수값  | 제한      |
| ------------------- | ------ | --------------------------------------------------------------- | ---- | ------- |
| sellerUnicroUserKey | String | 판매자 식별키                                                         | true |         |
| partnerItemNo       | String | 제휴사 상품고유식별번호                                                    | true |         |
| itemName            | String | 상품명                                                             | true | 200자 이내 |
| itemPrice           | Number | 상품가격                                                            | true | 3000 이상 |
| selPayway           | Array  | 결제가능한 결제수단 (CARD: 신용카드, BANK: 계좌이체, VIRTUAL\_ACCOUNT: 가상계좌 무통장) | true |         |
| deliveryPayCd       | String | 배송비부담 (CASH\_ON\_DELIVERY:착불(구매자부담), PRE\_PAYMENT:선불(판매자부담))    | true |         |
| imgUrl              | String | 이미지 경로 URI                                                      |      |         |
| mainCategoryCd      | String | 메인 카테고리 코드 (상품코드표 참고)                                           |      |         |
| subCategoryCd       | String | 서브 카테고리 코드 (상품코드표 참고)                                           |      |         |

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 233

{
  "result" : "SUCCESS",
  "msg" : "상품이 정상 등록되었습니다.",
  "errorCd" : "",
  "data" : {
    "unicroItemNo" : "220900609127",
    "partnerItemNo" : "22090701",
    "statusCd" : "AVAILABLE_FOR_SALE"
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

### 3. 거래(제휴사) <a href="#_3_" id="_3_"></a>

**3.1 제휴사 거래번호로 거래 조회**

***

제휴사 거래번호로 거래를 조회하는 API입니다.

* **기능** 제휴사 거래번호로 거래 조회
* **URI** /api/v1/traders/partner/{partnerTradeNo}
* **Method:** `GET`

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/traders/partner/2022045465' -i -X GET
```

**요청**

```
GET /api/v1/traders/partner/2022045465 HTTP/1.1
Host: stg-api.unicro.co.kr:14147
```

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 192

{
  "result" : "SUCCESS",
  "msg" : "",
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

**3.2 유니크로 거래번호로 거래 조회**

***

유니크로 거래번호로 거래를 조회하는 API입니다.

* **기능** 유니크로 거래번호로 거래 조회
* **URI** /api/v1/traders/{unicroTradeNo}
* **Method:** `GET`

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/traders/202204546555' -i -X GET
```

**요청**

```
GET /api/v1/traders/202204546555 HTTP/1.1
Host: stg-api.unicro.co.kr:14147
```

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 194

{
  "result" : "SUCCESS",
  "msg" : "",
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

**3.3 수동 배송완료 처리 (제휴사 관리자)**

***

제휴사 관리자가 수동으로 배송완료 처리하는 API입니다. 수동 배송완료 처리시 배송에 대한 책임은 제휴사에 있습니다.

**배송완료 처리가 가능한 거래상태**

| 상태            | 설명                       |
| ------------- | ------------------------ |
| PAY\_APPROVED | 요청 후 DELIVERY\_DONE로 변경됨 |
| DELIVERY\_ING | 요청 후 DELIVERY\_DONE로 변경됨 |

* **기능** 제휴사 관리자 배송완료 처리
* **URI** /api/v1/traders/{unicroTradeNo}/delivery/done
* **Method:** `POST`

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/traders/202209050000/delivery/done' -i -X POST
```

**요청**

```
POST /api/v1/traders/202209050000/delivery/done HTTP/1.1
Host: stg-api.unicro.co.kr:14147
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

### 4. 거래(구매자) <a href="#_4_" id="_4_"></a>

**4.1 구매자 결제 취소**

***

구매자가 결제 취소를 요청하는 API입니다.

**구매자 결제 취소가 가능한 거래상태**

| 상태            | 설명                                                       |
| ------------- | -------------------------------------------------------- |
| PAY\_STANDBY  | 요청 후 CANCEL\_DONE\_BUYER로 변경됨                            |
| PAY\_APPROVED | 요청 후 CANCEL\_REQ로 변경됨 (판매자가 취소요청을 승인하여야 거래취소 되는 상태로 변경됨) |

* **기능** 구매 취소 요청
* **URI** /api/v1/buyer/traders/{unicroTradeNo}/cancel
* **Method:** `POST`

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/buyer/traders/202209051745/cancel' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -d '{
  "buyerUnicroUserKey" : "UDdSfN5d525sD5FSD58",
  "cancelCd" : "",
  "cancelMemo" : "테스트용"
}'
```

**요청**

```
POST /api/v1/buyer/traders/202209051745/cancel HTTP/1.1
Content-Type: application/json
Accept: application/json
Content-Length: 106
Host: stg-api.unicro.co.kr:14147

{
  "buyerUnicroUserKey" : "UDdSfN5d525sD5FSD58",
  "cancelCd" : "",
  "cancelMemo" : "테스트용"
}
```

**Request Fields**

| 필드명                | 타입     | 설명         | 필수값  | 제한 |
| ------------------ | ------ | ---------- | ---- | -- |
| buyerUnicroUserKey | String | 구매자 식별키    | true |    |
| cancelCd           | String | 취소사유코드     | true |    |
| cancelMemo         | String | 취소사유(직접입력) |      |    |

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

**4.2 구매자 반품 요청**

***

구매자가 배송중인 거래를 반품요청하는 API입니다.

**구매자 반품요청이 가능한 거래상태**

| 상태            | 설명                    |
| ------------- | --------------------- |
| DELIVERY\_ING | 요청 후 RETURN\_REQ로 변경됨 |

* **기능** 구매자 반품 요청
* **URI** /api/v1/buyer/traders/{unicroTradeNo}/return/create
* **Method:** `POST`

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/buyer/traders/202209051745/return/create' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -d '{
  "buyerUnicroUserKey" : "UDdSfN5d525sD5FSD58",
  "returnDeliveryPayCd" : "CASH_ON_DELIVERY",
  "returnCd" : "",
  "returnMemo" : ""
}'
```

**요청**

```
POST /api/v1/buyer/traders/202209051745/return/create HTTP/1.1
Content-Type: application/json
Accept: application/json
Content-Length: 141
Host: stg-api.unicro.co.kr:14147

{
  "buyerUnicroUserKey" : "UDdSfN5d525sD5FSD58",
  "returnDeliveryPayCd" : "CASH_ON_DELIVERY",
  "returnCd" : "",
  "returnMemo" : ""
}
```

**Request Fields**

| 필드명                 | 타입     | 설명                                                 | 필수값  | 제한 |
| ------------------- | ------ | -------------------------------------------------- | ---- | -- |
| buyerUnicroUserKey  | String | 구매자 식별키                                            | true |    |
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

**4.3 구매자 반품 배송정보 기입**

***

구매자가 배송중인 거래를 반품요청하는 API입니다.

**구매자 반품 배송정보 기입이 가능한 거래상태**

| 상태            | 설명                    |
| ------------- | --------------------- |
| DELIVERY\_AGR | 요청 후 RETURN\_ING로 변경됨 |

* **기능** 구매자 반품 배송정보 기입
* **URI** /api/v1/buyer/traders/{unicroTradeNo}/return/delivery
* **Method:** `POST`

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/buyer/traders/202209051745/return/delivery' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -d '{
  "buyerUnicroUserKey" : "1234567",
  "deliveryCompCd" : "004",
  "invoiceNo" : "6044000000000",
  "returnSenderName" : "김다우",
  "returnSenderZip" : "16878",
  "returnSenderAddress1" : "경기 용인시 수지구 디지털벨리로 81 (죽전동, 다우기술)",
  "returnSenderAddress2" : "6층 플랫폼개발팀",
  "returnSenderHhpNo" : "01000001111"
}'
```

**요청**

```
POST /api/v1/buyer/traders/202209051745/return/delivery HTTP/1.1
Content-Type: application/json
Accept: application/json
Content-Length: 373
Host: stg-api.unicro.co.kr:14147

{
  "buyerUnicroUserKey" : "1234567",
  "deliveryCompCd" : "004",
  "invoiceNo" : "6044000000000",
  "returnSenderName" : "김다우",
  "returnSenderZip" : "16878",
  "returnSenderAddress1" : "경기 용인시 수지구 디지털벨리로 81 (죽전동, 다우기술)",
  "returnSenderAddress2" : "6층 플랫폼개발팀",
  "returnSenderHhpNo" : "01000001111"
}
```

**Request Fields**

| 필드명                  | 타입     | 설명                   | 필수값  | 제한 |
| -------------------- | ------ | -------------------- | ---- | -- |
| buyerUnicroUserKey   | String | 구매자 식별키              | true |    |
| deliveryCompCd       | String | 택배사 코드 (유니크로 코드표 참고) | true |    |
| invoiceNo            | String | 송장번호                 | true |    |
| returnSenderName     | String | 구매자명                 |      |    |
| returnSenderHhpNo    | String | 구매자 연락처              |      |    |
| returnSenderZip      | String | 구매자 우편번호             |      |    |
| returnSenderAddress1 | String | 구매자 주소1              |      |    |
| returnSenderAddress2 | String | 구매자 주소2              |      |    |

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

**4.4 거래 완료**

***

구매자가 상품을 받고 거래 완료처리하는 API입니다.

**거래 완료가 가능한 거래상태**

| 상태             | 설명                   |
| -------------- | -------------------- |
| DELIVERY\_ING  | 요청 후 PAY\_DONE으로 변경됨 |
| DELIVERY\_DONE | 요청 후 PAY\_DONE으로 변경됨 |

* **기능** 거래 완료
* **URI** /api/v1/buyer/traders/{unicroTradeNo}/done
* **Method:** `POST`

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/buyer/traders/202209051745/done' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -d '{
  "buyerUnicroUserKey" : "UDdSfN5d525sD5FSD58"
}'
```

**요청**

```
POST /api/v1/buyer/traders/202209051745/done HTTP/1.1
Content-Type: application/json
Accept: application/json
Content-Length: 52
Host: stg-api.unicro.co.kr:14147

{
  "buyerUnicroUserKey" : "UDdSfN5d525sD5FSD58"
}
```

**Request Fields**

| 필드명                | 타입     | 설명      | 필수값  | 제한 |
| ------------------ | ------ | ------- | ---- | -- |
| buyerUnicroUserKey | String | 구매자 식별키 | true |    |

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

**4.5 구매자 거래 상세 조회**

***

구매자가 거래 정보를 조회하는 API입니다.

* **기능** 구매자 거래 상세 조회
* **URI** /api/v1/buyer/traders/{unicroTradeNo}
* **Method:** `GET`

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/buyer/traders/202209050000?buyerUnicroUserKey=UDdSfN5d525sD5FSD51' -i -X GET
```

**요청**

```
GET /api/v1/buyer/traders/202209050000?buyerUnicroUserKey=UDdSfN5d525sD5FSD51 HTTP/1.1
Host: stg-api.unicro.co.kr:14147
```

| Parameter            | Description |
| -------------------- | ----------- |
| `buyerUnicroUserKey` | 구매자 식별키     |

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 618

{
  "result" : "SUCCESS",
  "msg" : "구매자 거래 조회에 성공했습니다.",
  "errorCd" : "",
  "data" : {
    "unicroTradeNo" : "202209050000",
    "partnerTradeNo" : "123456789",
    "payway" : "VIRTUAL_ACCOUNT",
    "buyAmt" : 3000,
    "tradeDate" : "2022-09-14T16:50:46.2300773",
    "statusCd" : "SETTLEMENT_DONE",
    "deliveryCompCd" : "",
    "invoiceNo" : "",
    "unicroItemNo" : "20220091300000",
    "partnerItemNo" : "2022009130000A0",
    "bankName" : "신한은행",
    "account" : "10000000000",
    "accountName" : "유니크로",
    "vaDate" : "202209150100000"
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
| data.account        | String | 입금정보-계좌번호                          |
| data.accountName    | String | 예금주                                |
| data.vaDate         | String | 무통장입금기한                            |

### 5. 거래(판매자) <a href="#_5_" id="_5_"></a>

**5.1 판매자 결제취소 동의**

***

판매자가 구매자 결제취소 요청에 동의하는 API입니다.

**판매자 결제취소 동의가 가능한 거래상태**

| 상태          | 설명                            |
| ----------- | ----------------------------- |
| CANCEL\_REQ | 요청 후 CANCEL\_DONE\_BUYER로 변경됨 |

* **기능** 판매자 결제취소 동의
* **URI** /api/v1/seller/traders/{unicroTradeNo}/cancel/agree
* **Method:** `POST`

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/seller/traders/202209050000/cancel/agree' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -d '{
  "sellerUnicroUserKey" : "UDdSfN5d525sD5FSD51"
}'
```

**요청**

```
POST /api/v1/seller/traders/202209050000/cancel/agree HTTP/1.1
Content-Type: application/json
Accept: application/json
Content-Length: 53
Host: stg-api.unicro.co.kr:14147

{
  "sellerUnicroUserKey" : "UDdSfN5d525sD5FSD51"
}
```

**Request Fields**

| 필드명                 | 타입     | 설명      | 필수값  | 제한 |
| ------------------- | ------ | ------- | ---- | -- |
| sellerUnicroUserKey | String | 판매자 식별키 | true |    |

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 253

{
  "result" : "SUCCESS",
  "msg" : "구매자 결제취소에 동의가 완료 되었습니다.",
  "errorCd" : "",
  "data" : {
    "unicroTradeNo" : "202209050000",
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

**5.2 판매자 거래취소**

***

판매자가 거래를 취소하는 API입니다.

**판매자 거래 취소가 가능한 거래상태**

| 상태            | 설명                             |
| ------------- | ------------------------------ |
| PAY\_APPROVED | 요청 후 CANCEL\_DONE\_SELLER로 변경됨 |

* **기능** 판매자 거래 취소
* **URI** /api/v1/seller/traders/{unicroTradeNo}/cancel/done
* **Method:** `POST`

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/seller/traders/202209050000/cancel/done' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -d '{
  "sellerUnicroUserKey" : "UDdSfN5d525sD5FSD51",
  "cancelCd" : "39",
  "cancelMemo" : "판매취소사유(직접입력)"
}'
```

**요청**

```
POST /api/v1/seller/traders/202209050000/cancel/done HTTP/1.1
Content-Type: application/json
Accept: application/json
Content-Length: 129
Host: stg-api.unicro.co.kr:14147

{
  "sellerUnicroUserKey" : "UDdSfN5d525sD5FSD51",
  "cancelCd" : "39",
  "cancelMemo" : "판매취소사유(직접입력)"
}
```

**Request Fields**

| 필드명                 | 타입     | 설명            | 필수값  | 제한      |
| ------------------- | ------ | ------------- | ---- | ------- |
| sellerUnicroUserKey | String | 판매자 식별키       | true |         |
| cancelCd            | String | 판매취소 사유코드     | true |         |
| cancelMemo          | String | 판매취소 사유(직접입력) |      | 500자 이내 |

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 245

{
  "result" : "SUCCESS",
  "msg" : "판매자 거래 취소가 완료 되었습니다.",
  "errorCd" : "",
  "data" : {
    "unicroTradeNo" : "202209050000",
    "partnerTradeNo" : "1224545",
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

**5.3 배송정보 기입**

***

판매자가 배송정보를 기입하는 API입니다.

**판매자 배송정보 기입이 가능한 거래상태**

| 상태            | 설명                      |
| ------------- | ----------------------- |
| PAY\_APPROVED | 요청 후 DELIVERY\_ING로 변경됨 |

* **기능** 판매자 배송정보 기입
* **URI** /api/v1/seller/traders/{unicroTradeNo}/delivery
* **Method:** `POST`

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/seller/traders/202209050000/delivery' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -d '{
  "sellerUnicroUserKey" : "UDdSfN5d525sD5FSD51",
  "partnerTradeNo" : "123456789",
  "deliveryPayCd" : "PRE_PAYMENT",
  "deliveryCompCd" : "005",
  "invoiceNo" : "1234567890",
  "senderName" : "권희수",
  "senderZip" : "16878",
  "senderAddress1" : "경기 용인시 수지구 디지털벨리로 81 (죽전동, 다우기술)",
  "senderAddress2" : "6층 플랫폼개발팀",
  "senderHhpNo" : "010-9939-2814"
}'
```

**요청**

```
POST /api/v1/seller/traders/202209050000/delivery HTTP/1.1
Content-Type: application/json
Accept: application/json
Content-Length: 426
Host: stg-api.unicro.co.kr:14147

{
  "sellerUnicroUserKey" : "UDdSfN5d525sD5FSD51",
  "partnerTradeNo" : "123456789",
  "deliveryPayCd" : "PRE_PAYMENT",
  "deliveryCompCd" : "005",
  "invoiceNo" : "1234567890",
  "senderName" : "권희수",
  "senderZip" : "16878",
  "senderAddress1" : "경기 용인시 수지구 디지털벨리로 81 (죽전동, 다우기술)",
  "senderAddress2" : "6층 플랫폼개발팀",
  "senderHhpNo" : "010-9939-2814"
}
```

**Request Fields**

| 필드명                 | 타입     | 설명                                              | 필수값  | 제한 |
| ------------------- | ------ | ----------------------------------------------- | ---- | -- |
| sellerUnicroUserKey | String | 판매자 식별키                                         | true |    |
| partnerTradeNo      | String | 제휴사 거래고유식별번호                                    | true |    |
| deliveryPayCd       | String | 판매자 택배 (CASH\_ON\_DELIVERY:착불, PRE\_PAYMENT:선불) | true |    |
| deliveryCompCd      | String | 택배사 코드 (유니크로 코드표 참고)                            | true |    |
| invoiceNo           | String | 송장번호                                            | true |    |
| senderName          | String | 판매자명                                            |      |    |
| senderHhpNo         | String | 판매자 연락처                                         |      |    |
| senderZip           | String | 판매자 우편번호                                        |      |    |
| senderAddress1      | String | 판매자 주소1                                         |      |    |
| senderAddress2      | String | 판매자 주소2                                         |      |    |

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

**5.4 반품 수락**

***

판매자가 구매자의 반품 요청을 수락하는 API입니다.

**반품 수락이 가능한 거래상태**

| 상태          | 설명                    |
| ----------- | --------------------- |
| RETURN\_REQ | 요청 후 RETURN\_AGR로 변경됨 |

* **기능** 반품 수락
* **URI** /api/v1/seller/traders/{unicroTradeNo}/return/agree
* **Method:** `POST`

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/seller/traders/202209050000/return/agree' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -d '{
  "sellerUnicroUserKey" : "UDdSfN5d525sD5FSD51",
  "partnerTradeNo" : "123456789",
  "senderName" : "권희수",
  "senderZip" : "16878",
  "senderAddress1" : "경기 용인시 수지구 디지털벨리로 81 (죽전동, 다우기술)",
  "senderAddress2" : "6층 플랫폼개발팀",
  "senderHhpNo" : "010-9939-2814"
}'
```

**요청**

```
POST /api/v1/seller/traders/202209050000/return/agree HTTP/1.1
Content-Type: application/json
Accept: application/json
Content-Length: 330
Host: stg-api.unicro.co.kr:14147

{
  "sellerUnicroUserKey" : "UDdSfN5d525sD5FSD51",
  "partnerTradeNo" : "123456789",
  "senderName" : "권희수",
  "senderZip" : "16878",
  "senderAddress1" : "경기 용인시 수지구 디지털벨리로 81 (죽전동, 다우기술)",
  "senderAddress2" : "6층 플랫폼개발팀",
  "senderHhpNo" : "010-9939-2814"
}
```

**Request Fields**

| 필드명                 | 타입     | 설명           | 필수값  | 제한 |
| ------------------- | ------ | ------------ | ---- | -- |
| sellerUnicroUserKey | String | 판매자 식별키      | true |    |
| partnerTradeNo      | String | 제휴사 거래고유식별번호 | true |    |
| senderName          | String | 판매자명         | true |    |
| senderHhpNo         | String | 판매자 연락처      | true |    |
| senderZip           | String | 판매자 우편번호     | true |    |
| senderAddress1      | String | 판매자 주소1      | true |    |
| senderAddress2      | String | 판매자 주소2      | true |    |

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

**5.5 반품 완료**

***

판매자가 반품 완료하는 API입니다.

**반품 완료가 가능한 거래상태**

| 상태          | 설명                     |
| ----------- | ---------------------- |
| RETURN\_AGR | 요청 후 RETURN\_DONE로 변경됨 |

* **기능** 반품 완료
* **URI** /api/v1/seller/traders/{unicroTradeNo}/return/done
* **Method:** `POST`

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/seller/traders/202209050000/return/done' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -d '{
  "sellerUnicroUserKey" : "UDdSfN5d525sD5FSD51"
}'
```

**요청**

```
POST /api/v1/seller/traders/202209050000/return/done HTTP/1.1
Content-Type: application/json
Accept: application/json
Content-Length: 53
Host: stg-api.unicro.co.kr:14147

{
  "sellerUnicroUserKey" : "UDdSfN5d525sD5FSD51"
}
```

**Request Fields**

| 필드명                 | 타입     | 설명      | 필수값  | 제한 |
| ------------------- | ------ | ------- | ---- | -- |
| sellerUnicroUserKey | String | 판매자 식별키 | true |    |

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 223

{
  "result" : "SUCCESS",
  "msg" : "반품완료 처리되었습니다.",
  "errorCd" : "",
  "data" : {
    "unicroTradeNo" : "202209050000",
    "partnerTradeNo" : "1224545",
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

**5.6 판매자 거래 상세 조회**

***

판매자가 거래 정보를 조회하는 API입니다.

* **기능** 판매자 거래 상세 조회
* **URI** /api/v1/seller/traders/{unicroTradeNo}
* **Method:** `GET`

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/seller/traders/202209050000?sellerUnicroUserKey=UDdSfN5d525sD5FSD51' -i -X GET
```

**요청**

```
GET /api/v1/seller/traders/202209050000?sellerUnicroUserKey=UDdSfN5d525sD5FSD51 HTTP/1.1
Host: stg-api.unicro.co.kr:14147
```

| Parameter             | Description |
| --------------------- | ----------- |
| `sellerUnicroUserKey` | 판매자 식별키     |

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 498

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
    "tradeDate" : "2022-09-14T16:50:47.3187563",
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