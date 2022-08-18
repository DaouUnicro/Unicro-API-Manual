##### 3.1. 구매하기 
----
구매자가 구매를 위해 호출하는 API입니다.

* **기능**
  구매요청

* **URI**
  /trades

* **Method:**
  `POST`

*  **URL Params**

  | 파라메터 | 설명 | 타입 | 필수 |
  |--|--|--|--|
  | itemNo | 유니크로 상품코드 | String | O |
  | aspTradeNo | 제휴사 거래번호 | String | O |
  | payway | 결제수단 (CARD: 신용카드, BANK: 계좌이체, VIRTUAL_ACCOUNT: 가상계좌 무통장) | String | O |
  | returnUrl | 결제 완료 후 URI | String | O |
  | deliveryPayType | 배송비부담 - 판매자 (CASH_ON_DELIVERY:착불, PRE_PAYMENT:선불(무료배송/택배비포함)) | String | O |
  | trCodeOpt | 현금영수증 (PERSON: 개인, BUSINESS: 사업자) | String | X |
  | cashInfo | 현금영수증 > 휴대번호| String | X |
  | cashInfo | 현금영수증 > 사업자번호| String | X |
  | buyerName | 구매자명 | String | X |
  | buyerMail | 구매자이메일 | String | X |
  | buyerHhpNo | 구매자휴대번호 | String | X |
  | deliveryZip | 배송주소(우편번호) | String | O |
  | deliveryAddress1 | 배송주소(주소1) | String | O |
  | deliveryAddress2 | 배송주소(주소2) | String | O |
  | appUrl | 앱 URI | String | X |
  | unicroUserNo | 유니크로 사용자 식별키로 유니크로 가입후 전달 한 값입니다.(구매자) | Integer | O |
  | userId|유니크로 아이디| String (4~75 byte 영문소문자, 숫자, @ _ . 만 가능(공백불가))(구매자) | O |

* **Success Response:**
      

* **Fail Response:**

##### 3.2. 구매자 거래취소

----
구매자가 구매한 거래를 취소 요청하는 API입니다.

###### 구매요청이 가능한 거래상태
  | 상태 | 설명 |
  |--|--|
  | PAY_STANDBY   | 요청 후 CANCEL_DONE_BUYER로 변경됨 |
  | PAY_APPROVED   | 요청 후 CANCEL_REQ로 변경됨 (판매자가 취소요청을 승인하여야 거래취소 되는 상태로 변경됨) |

* **기능**
  구매 취소 요청

* **URI**
  /trades/cancel

* **Method:**
  `POST`

*  **URL Params**

  | 파라메터 | 설명 | 타입 | 필수 |
  |--|--|--|--|
  | tradeNo|유니크로 거래번호 | String | O |
  | aspTradeNo|제휴사 거래번호 | String | O |
  | returnCd|거래취소사유코드 | String | X |
  | returnMemo|거래취소사유(직접입력) | String | X |
  | unicroUserNo|유니크로 사용자 식별키로 유니크로 가입후 전달 한 값입니다.(구매자) | Integer | O |

* **Success Response:**
  
* **Fail Response:**

##### 3.3. 거래 조회