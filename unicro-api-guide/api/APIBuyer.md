##### 3.1. 구매하기 
----
구매자가 구매를 위해 호출하는 API입니다.

* **기능**
  구매요청

* **URI**
  /buyer/trades

* **Method:**
  `POST`

*  **URL Params**

  | 파라메터 | 설명 | 타입 | 필수 |
  |--|--|--|--|
  | unicroUserKey | 구매자 식별키 (유니크로 사용자 식별키로 유니크로 가입후 전달 한 값입니다.) | Integer | O |
  | partnerUserId | 구매자 제휴사 아이디 | String (4~75 byte 영문소문자, 숫자, @ _ . 만 가능, 공백 불가) | O |
  | unicroItemNo | 유니크로 상품코드 | String | O |
  | partnerTradeNo | 제휴사 거래번호 | String | O |
  | payway | 결제수단 (CARD: 신용카드, BANK: 계좌이체, VIRTUAL_ACCOUNT: 가상계좌 무통장) | String | O |
  | returnUrl | 결제 완료 후 URI | String | O |
  | deliveryPayType | 배송비부담 - 판매자 (CASH_ON_DELIVERY:착불, PRE_PAYMENT:선불(무료배송/택배비포함)) | String | O |
  | trCodeOpt | 현금영수증 (PERSON: 개인, BUSINESS: 사업자) | String | X |
  | cashInfo | 현금영수증 > 휴대번호| String | X |
  | cashInfo | 현금영수증 > 사업자번호| String | X |
  | buyerName | 구매자명 | String | X |
  | buyerEmail | 구매자이메일 | String | X |
  | buyerHhpNo | 구매자휴대번호 | String | X |
  | deliveryZip | 배송주소(우편번호) | String | O |
  | deliveryAddress1 | 배송주소(주소1) | String | O |
  | deliveryAddress2 | 배송주소(주소2) | String | O |
  | appUrl | 앱 URI | String | X |

* **응답:**


##### 3.2. 구매자 결제 취소
----
구매자가 결제 취소를 요청하는 API입니다.

###### 구매요청이 가능한 거래상태
  | 상태 | 설명 |
  |--|--|
  | PAY_STANDBY   | 요청 후 CANCEL_DONE_BUYER로 변경됨 |
  | PAY_APPROVED   | 요청 후 CANCEL_REQ로 변경됨 (판매자가 취소요청을 승인하여야 거래취소 되는 상태로 변경됨) |

* **기능**
  구매 취소 요청

* **URI**
  /buyer/cancel

* **Method:**
  `POST`

*  **URL Params**

  | 파라메터        | 설명 | 타입 | 필수 |
  |--               | --|--|--|
  | unicroUserKey    | 구매자 식별키 (유니크로 사용자 식별키로 유니크로 가입후 전달 한 값입니다.) | String | O |
  | unicroTradeNo   | 유니크로 거래번호 | String | O |
  | partnerTradeNo  | 제휴사 거래번호 | String | O |
  | returnCd        | 거래취소사유코드 | String | X |
  | returnMemo      | 거래취소사유(직접입력) | String | X |

* **응답:**
```json
{
  "result": "SUCCESS",
  "msg": "구매 취소 요청이 완료 되었습니다.",
  "errorCd": "",
  "data": {
    "unicroTradeNo": "220822124545",
    "partnerTradeNo": "ABCK554545454"
  }
}

```

##### 3.3. 구매자 반품 요청
----
구매자가 배송중인 거래를 반품요청하는 API입니다.

###### 반품요청이 가능한 거래상태
  | 상태          | 설명 |
  |--             |--|
  | DELIVERY_ING  | 요청 후 RETURN_REQ로 변경됨 |

* **기능**
  구매자 반품 요청

* **URI**
  /buyer/reqReturn

* **Method:**
  `POST`

*  **URL Params**

  | 파라메터                | 설명 | 타입 | 필수 |
  |--                       |--|--|--|
  | unicroUserKey            | 구매자 식별키 (유니크로 사용자 식별키로 유니크로 가입후 전달한 값입니다.) | String | O |
  | partnerUserId           | 구매자 제휴사 아이디 | String (4~50자) | O |
  | partnerTradeNo          | 제휴사 거래고유식별번호 | String | O |
  | returnDeliveryPayType   | 반품 배송비 부담 (CASH_ON_DELIVERY:착불(판매자부담), PRE_PAYMENT:선불(구매자부담)) | String | X |
  | returnCd                | 반품 사유코드 | String | X |
  | returnMemo              | 반품 사유(직접입력) | String | X |

* **응답:**
```json
{
  "result": "SUCCESS",
  "msg": "반품요청이 완료 되었습니다.",
  "errorCd": "",
  "data": {
    "unicroTradeNo": "220822124545",
    "partnerTradeNo": "ABCK554545454"
  }
}

```

##### 3.4. 구매자 반품 배송정보 기입
----
구매자가 판매자 반품 수락 후 반품 배송정보를 기입하는 API입니다.

###### 반품요청이 가능한 거래상태
  | 상태        | 설명 |
  |--           |--|
  | RETURN_AGR  | 요청 후 RETURN_ING로 변경됨 |

* **기능**
  구매자 반품 배송정보 기입

* **URI**
  /buyer/returnDelivery

* **Method:**
  `POST`

*  **URL Params**

  | 파라메터        | 설명 | 타입 | 필수 |
  |--               |--|--|--|
  | unicroUserKey    | 구매자 식별키 (유니크로 사용자 식별키로 유니크로 가입후 전달한 값입니다.) | String | O |
  | partnerUserId   | 구매자 제휴사 아이디 | String (4~50자) | O |
  | partnerTradeNo  | 제휴사 거래고유식별번호 | String | O |
  | deliveryCompCd  | 택배사 코드 | String | O |
  | invoiceNo       | 송장번호 | String | O |

* **응답:**
```json
{
  "result": "SUCCESS",
  "msg": "배송정보 기입이 완료 되었습니다.",
  "errorCd": "",
  "data": {
    "unicroTradeNo": "220822124545",
    "partnerTradeNo": "ABCK554545454"
  }
}

```

##### 3.5. 거래 완료
----
구매자가 상품을 받고 거래 완료처리하는 API입니다.

###### 거래 완료가 가능한 거래상태
  | 상태            | 설명 |
  |--               |--|
  | DELIVERY_ING    | 요청 후 PAY_DONE으로 변경됨 |
  | DELIVERY_DONE   | 요청 후 PAY_DONE으로 변경됨 |

* **기능**
  거래 완료

* **URI**
  /buyer/doneTrade

* **Method:**
  `POST`

*  **URL Params**

  | 파라메터                | 설명 | 타입 | 필수 |
  |--                       |--|--|--|
  | unicroUserKey            | 구매자 식별키 (유니크로 사용자 식별키로 유니크로 가입후 전달한 값입니다.) | String | O |
  | partnerUserId           | 구매자 제휴사 아이디 | String (4~50자) | O |
  | partnerTradeNo          | 제휴사 거래고유식별번호 | String | O |

* **응답:**
```json
{
  "result": "SUCCESS",
  "msg": "반품요청이 완료 되었습니다.",
  "errorCd": "",
  "data": {
    "unicroTradeNo": "220822124545",
    "partnerTradeNo": "ABCK554545454"
  }
}

```

* **에러코드:**

| 파라메터 | 설명 |
|--|--|
| AUTH_CREATE_ERROR | 토큰 발급 실패 |
| VALID_ERROR | 필수 파라메터 없음 |


##### 3.6. 거래 조회
----
구매자가 거래를 조회하는 API입니다.

* **기능**
  구매자 거래 조회

* **URI**
  /buyer/trades

* **Method:**
  `GET`

*  **URL Params**

  | 파라메터 | 설명 | 타입 | 필수 |
  |--|--|--|--|
  | unicroUserKey | 구매자 식별키 (유니크로 사용자 식별키로 유니크로 가입후 전달 한 값입니다.) | String | O |
  | partnerTradeNo | 제휴사 거래고유식별번호 | String | O |

* **응답:**
```json
{
  "result": "SUCCESS",
  "msg": "반품요청이 완료 되었습니다.",
  "errorCd": "",
  "data": {
    "unicroTradeNo": "220822124545",
    "partnerTradeNo": "ABCK554545454",
    "payway": "CARD",
    "buyAmt": 5000,
    "sellerAmt": 4500,
    "tradeDate": "20220822171600",
    "vaExpectDate": "20220823171600",
    "vaBankCd": "008",
    "status": "PAY_APPROVED",
    "deliveryCompCd": "",
    "invoiceNo": "",
    "unicroItemNo": "220822121212",
    "partnerItemNo": "220822121212"
  }
}
```

