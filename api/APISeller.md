#### 4.1. 판매자 결제취소 동의
----
판매자가 구매자 결제취소 요청에 동의하는 API입니다. 

###### 판매자 결제취소 동의가 가능한 거래상태
  | 상태        | 설명 |
  |--           | --|
  | CANCEL_REQ  | 요청 후 CANCEL_DONE_BUYER로 변경됨 |

* **기능**
  판매자 결제취소 동의

* **URI**
  /seller/agreeCancel

* **Method:**
  `POST`

*  **URL Params**

  | 파라메터        | 설명 | 타입 | 필수 |
  |--               |--|--|--|
  | unicroUserNo    | 판매자 식별키 (유니크로 사용자 식별키로 유니크로 가입후 전달한 값입니다.) | Integer | O |
  | partnerUserId   | 판매자 제휴사 아이디 | String (4~50자) | O |
  | partnerTradeNo  | 제휴사 거래고유식별번호 | String | O |

* **Success Response:**
      

* **Fail Response:**

#### 4.2. 판매자 거래 취소
----
판매자가 거래를 취소하는 API입니다. 

###### 판매자 거래 취소가 가능한 거래상태
  | 상태            | 설명 |
  |--               | --|
  | PAY_APPROVED    | 요청 후 CANCEL_DONE_SELLER로 변경됨 |

* **기능**
  판매자 거래 취소

* **URI**
  /seller/cancel

* **Method:**
  `POST`

*  **URL Params**

  | 파라메터        | 설명 | 타입 | 필수 |
  |--               |--|--|--|
  | unicroUserNo    | 판매자 식별키 (유니크로 사용자 식별키로 유니크로 가입후 전달한 값입니다.) | Integer | O |
  | partnerUserId   | 판매자 제휴사 아이디 | String (4~50자) | O |
  | partnerTradeNo  | 제휴사 거래고유식별번호 | String | O |
  | cancelCd        | 판매취소 사유코드 | String | X |
  | cancelMemo      | 판매취소 사유(직접입력) | String | X |

* **Success Response:**
      
* **Fail Response:**

#### 4.3. 배송정보 기입
----
판매자가 배송정보를 기입하는 API입니다. 

###### 판매자 배송정보 기입이 가능한 거래상태
  | 상태            | 설명 |
  |--               | --|
  | PAY_APPROVED    | 요청 후 DELIVERY_ING로 변경됨 |

* **기능**
  판매자 배송정보 기입

* **URI**
  /seller/delivery

* **Method:**
  `POST`

*  **URL Params**

  | 파라메터        | 설명 | 타입 | 필수 |
  |--               |--|--|--|
  | unicroUserNo    | 판매자 식별키 (유니크로 사용자 식별키로 유니크로 가입후 전달한 값입니다.) | Integer | O |
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

* **Success Response:**
      
* **Fail Response:**

#### 4.4. 반품 수락
----
판매자가 구매자의 반품 요청을 수락하는 API입니다. 

###### 반품 수락이 가능한 거래상태
  | 상태        | 설명 |
  |--           | --|
  | RETURN_REQ  | 요청 후 RETURN_AGR로 변경됨 |

* **기능**
  반품 수락

* **URI**
  /seller/agreeReturn

* **Method:**
  `POST`

*  **URL Params**

  | 파라메터        | 설명 | 타입 | 필수 |
  |--               |--|--|--|
  | unicroUserNo    | 판매자 식별키 (유니크로 사용자 식별키로 유니크로 가입후 전달한 값입니다.) | Integer | O |
  | partnerUserId   | 판매자 제휴사 아이디 | String (4~50자) | O |
  | partnerTradeNo  | 제휴사 거래고유식별번호 | String | O |
  | senderName      | 판매자명 | String | O |
  | senderHhpNo     | 판매자 연락처 | String | O |
  | senderZip       | 판매자 우편번호 | String | O |
  | senderAddress1  | 판매자 주소1 | String | O |
  | senderAddress2  | 판매자 주소2 | String | O |

* **Success Response:**
      
* **Fail Response:**

#### 4.5. 반품 완료
----
판매자가 반품 완료하는 API입니다. 

###### 반품 완료가 가능한 거래상태
  | 상태        | 설명 |
  |--           | --|
  | RETURN_AGR  | 요청 후 RETURN_DONE로 변경됨 |

* **기능**
  반품 완료

* **URI**
  /seller/completeReturn

* **Method:**
  `POST`

*  **URL Params**

  | 파라메터        | 설명 | 타입 | 필수 |
  |--               |--|--|--|
  | unicroUserNo    | 판매자 식별키 (유니크로 사용자 식별키로 유니크로 가입후 전달한 값입니다.) | Integer | O |
  | partnerUserId   | 판매자 제휴사 아이디 | String (4~50자) | O |
  | partnerTradeNo  | 제휴사 거래고유식별번호 | String | O |

* **Success Response:**
      
* **Fail Response:**

#### 4.6. 배송완료처리(관리자)
----
#### 4.7. 거래 조회
----