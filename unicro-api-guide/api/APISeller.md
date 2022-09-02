# 4. 거래(판매자)

### 4.1. 판매자 결제취소 동의
----
판매자가 구매자 결제취소 요청에 동의하는 API입니다. 

###### 판매자 결제취소 동의가 가능한 거래상태
  | 상태        | 설명 |
  |--           | --|
  | CANCEL_REQ  | 요청 후 CANCEL_DONE_BUYER로 변경됨 |

* **기능**
  판매자 결제취소 동의

* **URI**
  /seller/traders/{unicroTradeNo}/cancel/agree

* **Method:**
  `POST`

*  **URL Params**

  | 파라메터        | 설명 | 타입 | 필수 |
  |--               |--|--|--|
  | sellerUnicroUserKey | 판매자 식별키 (유니크로 사용자 식별키로 유니크로 가입 후 전달한 판매자의 unicroUserKey 값입니다.) | String | O |
  | partnerUserId   | 판매자 제휴사 아이디 | String | O |
  | partnerTradeNo  | 제휴사 거래고유식별번호 | String | O |

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

### 4.2. 판매자 거래 취소
----
판매자가 거래를 취소하는 API입니다. 

###### 판매자 거래 취소가 가능한 거래상태
  | 상태            | 설명 |
  |--               | --|
  | PAY_APPROVED    | 요청 후 CANCEL_DONE_SELLER로 변경됨 |

* **기능**
  판매자 거래 취소

* **URI**  
  /seller/traders/{unicroTradeNo}/cancel/done

* **Method:**
  `POST`

*  **URL Params**

  | 파라메터        | 설명 | 타입 | 필수 |
  |--               |--|--|--|
  | sellerUnicroUserKey | 판매자 식별키 (유니크로 사용자 식별키로 유니크로 가입 후 전달한 판매자의 unicroUserKey 값입니다.) | String | O |
  | partnerUserId   | 판매자 제휴사 아이디 | String (4~50자) | O |
  | partnerTradeNo  | 제휴사 거래고유식별번호 | String | O |
  | cancelCd        | 판매취소 사유코드 | String | X |
  | cancelMemo      | 판매취소 사유(직접입력) | String | X |

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

### 4.3. 배송정보 기입
----
판매자가 배송정보를 기입하는 API입니다. 

###### 판매자 배송정보 기입이 가능한 거래상태
  | 상태            | 설명 |
  |--               | --|
  | PAY_APPROVED    | 요청 후 DELIVERY_ING로 변경됨 |

* **기능**
  판매자 배송정보 기입

* **URI**
  /seller/traders/{unicroTradeNo}/delivery

* **Method:**
  `POST`

*  **URL Params**

  | 파라메터        | 설명 | 타입 | 필수 |
  |--               |--|--|--|
  | sellerUnicroUserKey | 판매자 식별키 (유니크로 사용자 식별키로 유니크로 가입 후 전달한 판매자의 unicroUserKey 값입니다.) | String | O |
  | partnerUserId   | 판매자 제휴사 아이디 | String (4~50자) | O |
  | partnerTradeNo  | 제휴사 거래고유식별번호 | String | O |
  | deliveryPayType | 판매자 택배 (CASH_ON_DELIVERY:착불, PRE_PAYMENT:선불) | String | O |
  | deliveryCompCd  | 택배사 코드 | String | O |
  | invoiceNo       | 송장번호 | String | O |
  | senderName      | 보내는 사람 | String | X |
  | senderZip       | 보내는 사람 우편번호 | String | X |
  | senderAddress1  | 보내는 사람 주소1 | String | X |
  | senderAddress2  | 보내는 사람 주소2 | String | X |
  | senderHhpNo     | 보내는 사람 연락처 | String | X |

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

### 4.4. 반품 수락
----
판매자가 구매자의 반품 요청을 수락하는 API입니다. 

###### 반품 수락이 가능한 거래상태
  | 상태        | 설명 |
  |--           | --|
  | RETURN_REQ  | 요청 후 RETURN_AGR로 변경됨 |

* **기능**
  반품 수락

* **URI**
  /seller/traders/{unicroTradeNo}/return/agree

* **Method:**
  `POST`

*  **URL Params**

  | 파라메터        | 설명 | 타입 | 필수 |
  |--               |--|--|--|
  |sellerUnicroUserKey | 판매자 식별키 (유니크로 사용자 식별키로 유니크로 가입 후 전달한 판매자의 unicroUserKey 값입니다.) | String | O |
  | partnerUserId   | 판매자 제휴사 아이디 | String (4~50자) | O |
  | partnerTradeNo  | 제휴사 거래고유식별번호 | String | O |
  | senderName      | 판매자명 | String | O |
  | senderHhpNo     | 판매자 연락처 | String | O |
  | senderZip       | 판매자 우편번호 | String | O |
  | senderAddress1  | 판매자 주소1 | String | O |
  | senderAddress2  | 판매자 주소2 | String | O |

* **응답:**
```json
{
  "result": "SUCCESS",
  "msg": "반품수락이 완료 되었습니다.",
  "errorCd": "",
  "data": {
    "unicroTradeNo": "220822124545",
    "partnerTradeNo": "ABCK554545454"
  }
}

```
### 4.5. 반품 완료
----
판매자가 반품 완료하는 API입니다. 

###### 반품 완료가 가능한 거래상태
  | 상태        | 설명 |
  |--           | --|
  | RETURN_AGR  | 요청 후 RETURN_DONE로 변경됨 |

* **기능**
  반품 완료

* **URI**
  /seller/traders/{unicroTradeNo}/return/done

* **Method:**
  `POST`

*  **URL Params**

  | 파라메터        | 설명 | 타입 | 필수 |
  |--               |--|--|--|
  | sellerUnicroUserKey | 판매자 식별키 (유니크로 사용자 식별키로 유니크로 가입 후 전달한 판매자의 unicroUserKey 값입니다.) | String | O |
  | partnerUserId   | 판매자 제휴사 아이디 | String (4~50자) | O |
  | partnerTradeNo  | 제휴사 거래고유식별번호 | String | O |

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

### 4.6. 배송완료 처리 (제휴사 관리자)
----
배송정보 입력없이 배송완료 처리하는 API입니다. 
제휴사 관리자에서 사용이 가능하며 이 기능의 사용은 주의가 필요합니다.
배송정보없이 배송완료시 배송에 대한 책임은 제휴사에 있습니다.

###### 배송완료 처리가 가능한 거래상태
  | 상태            | 설명 |
  |--               | --|
  | PAY_APPROVED    | 요청 후 DELIVERY_DONE로 변경됨 |
  | DELIVERY_ING    | 요청 후 DELIVERY_DONE로 변경됨 |
  
* **기능**
  제휴사 관리자 배송완료 처리

* **URI**
  /partner/traders/{unicroTradeNo}/delivery/done
  
* **Method:**
  `POST`

*  **URL Params**

  | 파라메터        | 설명 | 타입 | 필수 |
  |--               |--|--|--|
  | sellerUnicroUserKey | 판매자 식별키 (유니크로 사용자 식별키로 유니크로 가입 후 전달한 판매자의 unicroUserKey 값입니다.) | String | O |
  | partnerTradeNo  | 제휴사 거래고유식별번호 | String | O |

* **응답:**
```json
{
  "result": "SUCCESS",
  "msg": "배송완료 처리가 완료 되었습니다.",
  "errorCd": "",
  "data": {
    "unicroTradeNo": "220822124545",
    "partnerTradeNo": "ABCK554545454"
  }
}

```

### 4.7. 판매자 거래 조회
----
판매자가 거래를 조회하는 API입니다.

* **기능**
  판매자 거래 조회

* **URI**
  /seller/traders/{unicroTradeNo}

* **Method:**
  `GET`

*  **URL Params**

  | 파라메터        | 설명 | 타입 | 필수 |
  |--               |--|--|--|
  | sellerUnicroUserKey | 판매자 식별키 (유니크로 사용자 식별키로 유니크로 가입 후 전달한 판매자의 unicroUserKey 값입니다.) | String | O |
  

* **Success Response:**
  | 파라메터        | 설명 | 타입 |
  |--               |-- | -- |
  | code            | 응답코드 | String |
  | msg             | 설명 메세지 | String |
  | data            |		
  | unicroTradeNo   | 유니크로 거래고유식별번호 | String (12자) |
  | partnerTradeNo  | 제휴사 거래고유식별번호 | String |
  | payway          | 결제수단 | String |
  | buyAmt          | 결제금액 | Integer |
  | sellerAmt       | 판매자 정산금액 | Integer |
  | tradeDate       | 결제일 | Date |
  | status          | 거래 상태 | String |
  | deliveryCompCd  | 택배사 코드 | String |
  | invoiceNo       | 송장번호 | String |  
  | unicroItemNo    | 유니크로 상품고유식별번호 | String |
  | partnerItemNo   | 제휴사 상품고유식별번호 | String |

* **응답:**
```json
{
  "result": "SUCCESS",
  "msg": "",
  "errorCd": "",
  "data": {
    "unicroTradeNo": "220822124545",
    "partnerTradeNo": "ABCK554545454",
    "payway": "CARD",
    "buyAmt" : 5000,
    "sellerAmt" : 4500,
    "tradeDate" : "20220824182002",
    "status" : "DELIVERY_DONE",
    "deliveryCompCd" : "002",
    "invoiceNo" : "566128065454",
    "unicroItemNo" : "220800609047",
    "partnerItemNo": "ABC800609047"
  }
}

```
