# API 상세

### 1. 인증 <a href="#_1_" id="_1_"></a>

**1.1 토큰 발급**

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
Content-Length: 119

{
  "result" : "SUCCESS",
  "msg" : "토큰 발급을 성공했습니다.",
  "errorCd" : "",
  "data" : "token"
}
```

**Response Fields**

| 필드명     | 타입     | 설명                                 |
| ------- | ------ | ---------------------------------- |
| result  | String | 성공실패 여부 코드 (성공: SUCCESS, 실패: FAIL) |
| msg     | String | 응답 메시지                             |
| errorCd | String | 실패시 에러 코드                          |
| data    | String | 전달 Data                            |

### 2. 상품(판매자) <a href="#_2_" id="_2_"></a>

**2.1 상품 등록**

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

### 3. 거래 <a href="#_3_" id="_3_"></a>

**3.1 제휴사거래번호로 거래조회**

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

**3.2 유니크로거래번호로 거래조회**

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

### 4. 거래(구매자) <a href="#_4_" id="_4_"></a>

**4.1 구매하기**

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/buyer/traders' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -d '{
  "buyerUnicroUserKey" : "1212",
  "unicroItemNo" : "12345678",
  "partnerTradeNo" : "1234564",
  "payway" : "VARTUAL_ACCOUNT",
  "returnUrl" : "",
  "deliveryPayCd" : "CASH_ON_DELIVERY",
  "tcCodeOpt" : "PERSON",
  "cashInfo" : "01012341234",
  "buyerName" : "김다우",
  "buyerEmail" : "unicro@daou.co.kr",
  "buyerHhpNo" : "01012341234",
  "deliveryZip" : "16878",
  "deliveryAddress1" : "",
  "deliveryAddress2" : "",
  "appUrl" : ""
}'
```

**요청**

```
POST /api/v1/buyer/traders HTTP/1.1
Content-Type: application/json
Accept: application/json
Content-Length: 459
Host: stg-api.unicro.co.kr:14147

{
  "buyerUnicroUserKey" : "1212",
  "unicroItemNo" : "12345678",
  "partnerTradeNo" : "1234564",
  "payway" : "VARTUAL_ACCOUNT",
  "returnUrl" : "",
  "deliveryPayCd" : "CASH_ON_DELIVERY",
  "tcCodeOpt" : "PERSON",
  "cashInfo" : "01012341234",
  "buyerName" : "김다우",
  "buyerEmail" : "unicro@daou.co.kr",
  "buyerHhpNo" : "01012341234",
  "deliveryZip" : "16878",
  "deliveryAddress1" : "",
  "deliveryAddress2" : "",
  "appUrl" : ""
}
```

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 607

{
  "result" : "SUCCESS",
  "msg" : "구매 요청이 완료 되었습니다.",
  "errorCd" : "",
  "data" : {
    "buyerUnicroUserKey" : "1212",
    "unicroItemNo" : "12345678",
    "partnerTradeNo" : "1234564",
    "payway" : "VARTUAL_ACCOUNT",
    "returnUrl" : "",
    "deliveryPayCd" : "CASH_ON_DELIVERY",
    "tcCodeOpt" : "PERSON",
    "cashInfo" : "01012341234",
    "buyerName" : "김다우",
    "buyerEmail" : "unicro@daou.co.kr",
    "buyerHhpNo" : "01012341234",
    "deliveryZip" : "16878",
    "deliveryAddress1" : "",
    "deliveryAddress2" : "",
    "appUrl" : ""
  }
}
```

**4.2 구매자 결제 취소**

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/buyer/traders/202209051745/cancel' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -d '{
  "buyerUnicroUserKey" : "1234",
  "unicroTradeNo" : "202209051745",
  "partnerTradeNo" : "ABNC302ABNC302",
  "returnCd" : "",
  "returnMemo" : "테스트용"
}'
```

**요청**

```
POST /api/v1/buyer/traders/202209051745/cancel HTTP/1.1
Content-Type: application/json
Accept: application/json
Content-Length: 168
Host: stg-api.unicro.co.kr:14147

{
  "buyerUnicroUserKey" : "1234",
  "unicroTradeNo" : "202209051745",
  "partnerTradeNo" : "ABNC302ABNC302",
  "returnCd" : "",
  "returnMemo" : "테스트용"
}
```

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 286

{
  "result" : "SUCCESS",
  "msg" : "구매 취소 되었습니다.",
  "errorCd" : "",
  "data" : {
    "buyerUnicroUserKey" : "1234",
    "unicroTradeNo" : "202209051745",
    "partnerTradeNo" : "ABNC302ABNC302",
    "returnCd" : "",
    "returnMemo" : "테스트용"
  }
}
```

**4.3 구매자 반품 요청**

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/buyer/traders/202209051745/return/create' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -d '{
  "buyerUnicroUserKey" : "1234",
  "unicroTradeNo" : "202209051745",
  "partnerTradeNo" : "ABNC302ABNC302",
  "returnCd" : "",
  "returnMemo" : ""
}'
```

**요청**

```
POST /api/v1/buyer/traders/202209051745/return/create HTTP/1.1
Content-Type: application/json
Accept: application/json
Content-Length: 156
Host: stg-api.unicro.co.kr:14147

{
  "buyerUnicroUserKey" : "1234",
  "unicroTradeNo" : "202209051745",
  "partnerTradeNo" : "ABNC302ABNC302",
  "returnCd" : "",
  "returnMemo" : ""
}
```

**Request Fields**

| 필드명                | 타입     | 설명           | 필수값  | 제한 |
| ------------------ | ------ | ------------ | ---- | -- |
| buyerUnicroUserKey | String | 구매자 식별키      | true |    |
| partnerTradeNo     | String | 제휴사 거래고유식별번호 | true |    |
| unicroTradeNo      | String | 유니크로거래번호     | true |    |
| returnCd           | String | 반품 사유코드      | true |    |
| returnMemo         | String | 반품 사유(직접입력)  |      |    |

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 283

{
  "result" : "SUCCESS",
  "msg" : "반품요청이 완료 되었습니다.",
  "errorCd" : "",
  "data" : {
    "buyerUnicroUserKey" : "1234",
    "unicroTradeNo" : "202209051745",
    "partnerTradeNo" : "ABNC302ABNC302",
    "returnCd" : "",
    "returnMemo" : ""
  }
}
```

**4.4 구매자 반품 배송정보 기입**

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/buyer/traders/202209051745/return/delivery' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -d '{
  "buyerUnicroUserKey" : null,
  "unicroTradeNo" : "202209051745",
  "partnerTradeNo" : "1224545",
  "deliveryCompCd" : null,
  "invoiceNo" : null
}'
```

**요청**

```
POST /api/v1/buyer/traders/202209051745/return/delivery HTTP/1.1
Content-Type: application/json
Accept: application/json
Content-Length: 156
Host: stg-api.unicro.co.kr:14147

{
  "buyerUnicroUserKey" : null,
  "unicroTradeNo" : "202209051745",
  "partnerTradeNo" : "1224545",
  "deliveryCompCd" : null,
  "invoiceNo" : null
}
```

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 297

{
  "result" : "SUCCESS",
  "msg" : "반품 배송정보 기입이 완료 되었습니다.",
  "errorCd" : "",
  "data" : {
    "buyerUnicroUserKey" : null,
    "unicroTradeNo" : "202209051745",
    "partnerTradeNo" : "1224545",
    "deliveryCompCd" : null,
    "invoiceNo" : null
  }
}
```

**4.5 거래 완료**

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/buyer/traders/202209051745/done' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -d '{
  "buyerUnicroUserKey" : "1234",
  "unicroTradeNo" : "202209051745",
  "partnerTradeNo" : "ABNC302ABNC302",
  "returnCd" : "",
  "returnMemo" : ""
}'
```

**요청**

```
POST /api/v1/buyer/traders/202209051745/done HTTP/1.1
Content-Type: application/json
Accept: application/json
Content-Length: 156
Host: stg-api.unicro.co.kr:14147

{
  "buyerUnicroUserKey" : "1234",
  "unicroTradeNo" : "202209051745",
  "partnerTradeNo" : "ABNC302ABNC302",
  "returnCd" : "",
  "returnMemo" : ""
}
```

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 277

{
  "result" : "SUCCESS",
  "msg" : "거래가 완료 되었습니다.",
  "errorCd" : "",
  "data" : {
    "buyerUnicroUserKey" : "1234",
    "unicroTradeNo" : "202209051745",
    "partnerTradeNo" : "ABNC302ABNC302",
    "returnCd" : "",
    "returnMemo" : ""
  }
}
```

### 5. 거래(판매자) <a href="#_5_" id="_5_"></a>

**5.1 판매자 결제취소 동의**

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/seller/traders/202209050000/cancel/agree' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -d '{
  "sellerUnicroUserKey" : "UDdSfN5d525sD5FSD51",
  "partnerTradeNo" : "123456789"
}'
```

**요청**

```
POST /api/v1/seller/traders/202209050000/cancel/agree HTTP/1.1
Content-Type: application/json
Accept: application/json
Content-Length: 88
Host: stg-api.unicro.co.kr:14147

{
  "sellerUnicroUserKey" : "UDdSfN5d525sD5FSD51",
  "partnerTradeNo" : "123456789"
}
```

**Request Fields**

| 필드명                 | 타입     | 설명           | 필수값  | 제한 |
| ------------------- | ------ | ------------ | ---- | -- |
| sellerUnicroUserKey | String | 판매자 식별키      | true |    |
| partnerTradeNo      | String | 제휴사 거래고유식별번호 | true |    |

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

**5.2 판매자 거래취소**

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/seller/traders/202209050000/cancel/done' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -d '{
  "sellerUnicroUserKey" : "UDdSfN5d525sD5FSD51",
  "partnerTradeNo" : "123456789",
  "cancelCd" : "39",
  "cancelMemo" : "판매취소사유(직접입력)"
}'
```

**요청**

```
POST /api/v1/seller/traders/202209050000/cancel/done HTTP/1.1
Content-Type: application/json
Accept: application/json
Content-Length: 164
Host: stg-api.unicro.co.kr:14147

{
  "sellerUnicroUserKey" : "UDdSfN5d525sD5FSD51",
  "partnerTradeNo" : "123456789",
  "cancelCd" : "39",
  "cancelMemo" : "판매취소사유(직접입력)"
}
```

**Request Fields**

| 필드명                 | 타입     | 설명            | 필수값  | 제한      |
| ------------------- | ------ | ------------- | ---- | ------- |
| sellerUnicroUserKey | String | 판매자 식별키       | true |         |
| partnerTradeNo      | String | 제휴사 거래고유식별번호  | true |         |
| cancelCd            | String | 판매취소 사유코드     | true |         |
| cancelMemo          | String | 판매취소 사유(직접입력) |      | 500자 이내 |

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

**5.3 배송정보 기입**

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

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/seller/traders/202209050000/return/done' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -d '{
  "sellerUnicroUserKey" : "UDdSfN5d525sD5FSD51",
  "partnerTradeNo" : "123456789"
}'
```

**요청**

```
POST /api/v1/seller/traders/202209050000/return/done HTTP/1.1
Content-Type: application/json
Accept: application/json
Content-Length: 88
Host: stg-api.unicro.co.kr:14147

{
  "sellerUnicroUserKey" : "UDdSfN5d525sD5FSD51",
  "partnerTradeNo" : "123456789"
}
```

**Request Fields**

| 필드명                 | 타입     | 설명           | 필수값  | 제한 |
| ------------------- | ------ | ------------ | ---- | -- |
| sellerUnicroUserKey | String | 판매자 식별키      | true |    |
| partnerTradeNo      | String | 제휴사 거래고유식별번호 | true |    |

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

**5.6 배송완료 처리(제휴사관리자)**

```
$ curl 'https://stg-api.unicro.co.kr:14147/api/v1/seller/traders/202209050000/delivery/done' -i -X POST \
    -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -d '{
  "sellerUnicroUserKey" : "UDdSfN5d525sD5FSD51",
  "partnerTradeNo" : "123456789"
}'
```

**요청**

```
POST /api/v1/seller/traders/202209050000/delivery/done HTTP/1.1
Content-Type: application/json
Accept: application/json
Content-Length: 88
Host: stg-api.unicro.co.kr:14147

{
  "sellerUnicroUserKey" : "UDdSfN5d525sD5FSD51",
  "partnerTradeNo" : "123456789"
}
```

**Request Fields**

| 필드명                 | 타입     | 설명           | 필수값  | 제한 |
| ------------------- | ------ | ------------ | ---- | -- |
| sellerUnicroUserKey | String | 판매자 식별키      | true |    |
| partnerTradeNo      | String | 제휴사 거래고유식별번호 | true |    |

**응답**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 227

{
  "result" : "SUCCESS",
  "msg" : "배송완료 처리되었습니다.",
  "errorCd" : "",
  "data" : {
    "unicroTradeNo" : "202209050000",
    "partnerTradeNo" : "123456789",
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

**5.7 판매자 거래 상세 조회**

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
    "tradeDate" : "2022-09-13T14:28:47.6647702",
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
