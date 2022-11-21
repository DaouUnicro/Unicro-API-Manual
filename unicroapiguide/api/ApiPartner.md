---
description: 제휴사측 개발이 필요한 API
---

# 제휴사 개발 API

### 7.0 유니크로 사용자 식별키 전달

유니크로 회원가입 후 unicroUserKey(유니크로 사용자 식별키)를 전달하기 위해 호출하는 API입니다.

* **기능** 유니크로 사용자 식별키 전달
* **URI**
* **Method:** `POST`
* **URL Params**

| 파라메터          | 설명                                       | 타입      |
| ------------- |------------------------------------------| ------- |
| unicroUserKey | 유니크로 사용자 식별키                             |  String |
| partnerUserId | <p>제휴사 사용자 이메일</p><p>(유니크로 회원가입 아이디)</p> | String  |

* **응답**

```
{
  "result": "SUCCESS",
  "msg": "unicroUserKey 저장 성공했습니다.",
  "errorCd": ""
}
```

****

### 7.1. 제휴사 토큰 발급

***

유니크로 토큰 발급 요청 후 제휴사측 토큰 발급 API를 요청하여 이중 체크를 하기 위한 API입니다.

* **기능** 제휴사 토큰 발급
* **URI**
* **Method:** `POST`
* **URL Params**

| 파라메터          | 설명                                | 타입                                        | 필수 |
| ------------- | --------------------------------- | ----------------------------------------- | -- |
| unicroUserKey | 유니크로 사용자 식별키로 유니크로 가입 후 전달한 값입니다. | String                                    | O  |
| partnerUserId | 유니크로 아이디                          | String (6\~75 byte 영문소문자, 숫자, 만 가능(공백불가)) | O  |

* **응답:**

<pre class="language-json"><code class="lang-json"><strong>{
</strong>  "result": "SUCCESS",
  "msg": "토큰 발급을 성공했습니다.",
  "errorCd": "",
  "data": {
    "unicroToken": "ABCDEFG"
  }
}</code></pre>

### 7.2. 결제 완료 후 성공시 전달

***

결제 완료 후 성공시 전달 받을 API 입니다.

* **기능** 구매자 결제 결과 전달 (성공시)
* **URI**
* **Method:** `POST`
* **URL Params**

| 파라메터           | 설명                                                        | 타입           | 필수 |
| -------------- | --------------------------------------------------------- | ------------ | -- |
| unicroTradeNo  | 유니크로 주문번호                                                 | String       | O  |
| partnerTradeNo | 제휴사 주문번호                                                  | String       | O  |
| payway         | 결제수단 (CARD: 신용카드, BANK: 계좌이체, VIRTUAL\_ACCOUNT: 가상계좌 무통장) | String       | O  |
| vaDate         | 무통장입금 입금기한(결제일 + 24시간)                                    | String(14자리) | X  |
| bankName       | 무통장입금 은행명                                                 | String       | X  |
| accountNo      | 무통장입금 가상계좌번호                                              | String       | X  |
| buyAmt         | 거래 금액                                                     | Integer      | O  |
| cardName       | 카드사명                                                      | Integer      | X  |
| itemName       | 상품명                                                       | String       | O  |

* **Success Response:**
* **Fail Response:**

### 7.3. 결제 완료 후 실패시 전달

***

결제 완료 후 실패시 전달 받을 API 입니다.

* **기능** 구매자 결제 결과 전달 (실패시)
* **URI**
* **Method:** `POST`
* **URL Params**

| 파라메터           | 설명        | 타입     | 필수 |
| -------------- | --------- | ------ | -- |
| unicroTradeNo  | 유니크로 주문번호 | String | O  |
| partnerTradeNo | 제휴사 주문번호  | String | O  |
| msg            | 결제실패 사유   | String | O  |

* **Success Response:**
* **Fail Response:**

### 7.4. 무통장 입금완료

***

가상계좌 신청 후 입금이 완료 된 경우 제휴사측에 전달하는 API입니다.

* **기능** 가상계좌 신청 후 입금이 완료 된 경우 제휴사측에 전달
* **URI**
* **Method:** `POST`
* **URL Params**

| 파라메터           | 설명        | 타입     | 필수 |
| -------------- | --------- | ------ | -- |
| unicroTradeNo  | 유니크로 주문번호 | String | O  |
| partnerTradeNo | 제휴사 주문번호  | String | O  |
| msg            | 결제실패 사유   | String | O  |

* **Success Response:**
* **Fail Response:**

### 7.5. 출금일자 전달 - 판매대금지급예정일, 판매대금지급완료일

***

거래 완료 후 제휴사측에 전달하는 API입니다.

* **기능** 거래 완료 후 출금예정일, 출금완료 후 판매대금지급 완료일을 전달하는 API입니다.
* **URI**
* **Method:** `POST`
* **URL Params**

| 파라메터                | 설명        | 타입     | 필수 |
| ------------------- | --------- | ------ | -- |
| unicroTradeNo       | 유니크로 주문번호 | String | O  |
| partnerTradeNo      | 제휴사 주문번호  | String | O  |
| saleReservationDate | 판매대금예정일   | String | O  |
| saleCompleteDate    | 판매대금완료일   | String | O  |
| sellerAmt    | 판매대금   | Integer | O  |

* **Success Response:**
* **Fail Response:**

### 7.6. \[관리자] 거래 취소

***

가상계좌 신청 후 입금이 완료 된 경우 제휴사측에 전달하는 API입니다.

* **기능** 거래 완료 후 출금예정일, 출금완료 후 판매대금지급 완료일을 전달하는 API입니다.
* **URI**
* **Method:** `POST`
* **URL Params**

| 파라메터           | 설명        | 타입     | 필수 |
| -------------- | --------- | ------ | -- |
| unicroTradeNo  | 유니크로 주문번호 | String | O  |
| partnerTradeNo | 제휴사 주문번호  | String | O  |
| returnCd       | 취소코드      | String | O  |
| returnMemo     | 취소사유      | String | O  |

* **Success Response:**
* **Fail Response:**

### 7.7. \[관리자] 택배정보 입력

***

가상계좌 신청 후 입금이 완료 된 경우 제휴사측에 전달하는 API입니다.

* **기능** 거래 완료 후 출금예정일, 출금완료 후 판매대금지급 완료일을 전달하는 API입니다.
* **URI**
* **Method:** `POST`
* **URL Params**

| 파라메터             | 설명         | 타입     | 필수 |
| ---------------- | ---------- | ------ | -- |
| unicroTradeNo    | 유니크로 주문번호  | String | O  |
| partnerTradeNo   | 제휴사 주문번호   | String | O  |
| senderEmail      | 보내는 사람 이메일 | String | O  |
| receiverName     | 받는사람 이름    | String | O  |
| receiverZip      | 받는사람 우편번호  | String | O  |
| receiverAddress1 | 받는사람 주소    | String | O  |
| receiverAddress2 | 받는사람 주소    | String | O  |
| receiverHhpNo    | 받는사람 연락처   | String | O  |
| deliveryCompCd   | 택배사코드      | String | O  |
| invoiceNo        | 송장번호       | String | O  |

* **Success Response:**
* **Fail Response:**

### 7.8. \[관리자] 반품택배정보 수정

***

### 7.9. \[관리자] 받는사람 정보 수정(일반)

***

### 7.10. \[관리자] 받는사람 정보 수정(반품)

***

### 7.11. 거래상태 변경 (단건/다건)

***
