### 5.1. 결제 완료 후 성공시 전달 받을 페이지(없다면 제휴사 default 결제완료)
----
결제 완료 후 성공시 전달 받을 API 입니다. (API/ 화면)
- API 형태 : API형태로만 만들고 화면은 만들지 않는다면 기본적으로 유니크로에서 제공되는 결제완료 페이지가 뜨도록 처리가 가능합니다.
- 화면 형태 : 전달된 파라메터를 이용해서 결제 완료 화면을 개발하면 됩니다.

* **기능**
  구매자 결제 결과 전달 (성공시)

* **URI**

* **Method:**
  `POST`

*  **URL Params**

  | 파라메터        | 설명 | 타입 | 필수 |
  |--               |--|--|--|
  | tradeNo    | 유니크로 주문번호 | String | O |
  | aspTradeNo    | 제휴사 주문번호 | String | O |
  | payType    | 결제수단 (CARD: 신용카드, BANK: 계좌이체, VIRTUAL_ACCOUNT: 가상계좌 무통장) | String | O |
  | vaDate   | 무통장입금 입금기한(결제일 + 24시간) | String(14자리) | X |
  | bankName  | 무통장입금 은행명 | String | X |
  | accountNo  | 무통장입금 가상계좌번호 | String | X |
  | buyAmt  | 거래 금액 | Integer | O |
  | cardName  | 카드사명 | Integer | X |
  | itemName  | 상품명 | String | O |

* **Success Response:**
      

* **Fail Response:**

### 5.2. 결제 완료 후 실패시 전달 받을 페이지(없다면 제휴사 default 결제실패)
----
결제 완료 후 성공시 전달 받을 API 입니다. (API/ 화면)
- API 형태 : API형태로만 만들고 화면은 만들지 않는다면 기본적으로 유니크로에서 제공되는 결제완료 페이지가 뜨도록 처리가 가능합니다.
- 화면 형태 : 전달된 파라메터를 이용해서 결제 완료 화면을 개발하면 됩니다.


* **기능**
  구매자 결제 결과 전달 (실패시)

* **URI**

* **Method:**
  `POST`

*  **URL Params**

  | 파라메터        | 설명 | 타입 | 필수 |
  |--               |--|--|--|
  | tradeNo    | 유니크로 주문번호 | String | O |
  | aspTradeNo    | 제휴사 주문번호 | String | O |
  | msg    | 결제실패 사유 | String | O |
  

* **Success Response:**
      

* **Fail Response:**

### 5.3. 무통장 입금완료
----
가상계좌 신청 후 입금이 완료 된 경우 제휴사측에 전달하는 API입니다.

* **기능**
  가상계좌 신청 후 입금이 완료 된 경우 제휴사측에 전달

* **URI**

* **Method:**
  `POST`

*  **URL Params**

  | 파라메터        | 설명 | 타입 | 필수 |
  |--               |--|--|--|
  | tradeNo    | 유니크로 주문번호 | String | O |
  | aspTradeNo    | 제휴사 주문번호 | String | O |
  | msg    | 결제실패 사유 | String | O |
  

* **Success Response:**
      

* **Fail Response:**

### 5.4. 출금일자 전달 - 판매대금지급예정일, 판매대금지급완료일
----
가상계좌 신청 후 입금이 완료 된 경우 제휴사측에 전달하는 API입니다.

* **기능**
  거래 완료 후 출금예정일, 출금완료 후 판매대금지급 완료일을 전달하는 API입니다.

* **URI**

* **Method:**
  `POST`

*  **URL Params**

  | 파라메터        | 설명 | 타입 | 필수 |
  |--               |--|--|--|
  | tradeNo    | 유니크로 주문번호 | String | O |
  | aspTradeNo    | 제휴사 주문번호 | String | O |
  | saleReservationDate    | 판매대금예정일 | String | O |
  | saleCompleteDate    | 판매대금완료일 | String | O |
    

* **Success Response:**
      
* **Fail Response:**
### 5.5. [관리자] 거래 취소
----
가상계좌 신청 후 입금이 완료 된 경우 제휴사측에 전달하는 API입니다.

* **기능**
  거래 완료 후 출금예정일, 출금완료 후 판매대금지급 완료일을 전달하는 API입니다.

* **URI**

* **Method:**
  `POST`

*  **URL Params**

  | 파라메터        | 설명 | 타입 | 필수 |
  |--               |--|--|--|
  | tradeNo    | 유니크로 주문번호 | String | O |
  | aspTradeNo    | 제휴사 주문번호 | String | O |
  | returnCd   | 취소코드 | String | O |
  | returnMemo    | 취소사유 | String | O |
    

* **Success Response:**
      
* **Fail Response:**
### 5.6. [관리자] 택배정보 입력
----
가상계좌 신청 후 입금이 완료 된 경우 제휴사측에 전달하는 API입니다.

* **기능**
  거래 완료 후 출금예정일, 출금완료 후 판매대금지급 완료일을 전달하는 API입니다.

* **URI**

* **Method:**
  `POST`

*  **URL Params**

  | 파라메터        | 설명 | 타입 | 필수 |
  |--               |--|--|--|
  | tradeNo    | 유니크로 주문번호 | String | O |
  | aspTradeNo    | 제휴사 주문번호 | String | O |
  | senderEmail   | 보내는 사람 이메일 | String | O |
  | receiverNam    | 받는사람 이름 | String | O |
  | receiverZip    | 받는사람 우편번호 | String | O |
  | receiverAddress1    | 받는사람 주소 | String | O |
  | receiverAddress2    | 받는사람 주소 | String | O |
  | receiverHhpNo    | 받는사람 연락처 | String | O |
  | deliveryCompCd    | 택배사코드 | String | O |
  | invoiceNo    | 송장번호 | String | O |
    

* **Success Response:**
      
* **Fail Response:**
### 5.7. [관리자] 반품택배정보 수정
----
### 5.8. [관리자] 받는사람 정보 수정(일반)
----
### 5.9. [관리자] 받는사람 정보 수정(반품)
----
### 5.10. 거래상태 변경 (단건/다건)
----
