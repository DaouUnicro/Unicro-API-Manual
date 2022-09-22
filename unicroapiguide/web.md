# 웹

### 1. 회원가입

### 2. 결제하기

***

구매자가 상품 구매를 위한 유니크로 결제화면입니다.

* **기능** 결제하기
* **URI** /buyer/trades
* **전달이 필요한 Params**

| 파라메터               | 설명                                                               | 타입     | 필수 |
| ------------------ | ---------------------------------------------------------------- | ------ | -- |
| buyerUnicroUserKey | 구매자 식별키 (유니크로 사용자 식별키로 유니크로 가입 후 전달한 구매자의 unicroUserKey 값입니다.)   | String | O  |
| unicroItemNo       | 유니크로 상품고유식별번호                                                     | String | O  |
| partnerTradeNo     | 제휴사 거래고유식별번호                                                     | String | O  |
| payway             | 결제수단 (CARD: 신용카드, BANK: 계좌이체, VIRTUAL_ACCOUNT: 가상계좌 무통장)        | String | O  |
| returnUrl          | 결제 완료 후 URI                                                      | String | O  |
| deliveryPayCd      | 배송비부담 - 판매자 (CASH_ON_DELIVERY:착불, PRE_PAYMENT:선불(무료배송/택배비포함)) | String | O  |
| trCodeOpt          | 현금영수증 (PERSON: 개인, BUSINESS: 사업자)                                | String | X  |
| cashInfo           | 현금영수증 > 휴대폰번호                                                     | String | X  |
| cashInfo           | 현금영수증 > 사업자번호                                                    | String | X  |
| buyerName          | 구매자명                                                             | String | X  |
| buyerEmail         | 구매자이메일                                                           | String | X  |
| buyerHhpNo         | 구매자휴대번호                                                          | String | X  |
| deliveryZip        | 배송주소(우편번호)                                                       | String | O  |
| deliveryAddress1   | 배송주소(주소1)                                                        | String | O  |
| deliveryAddress2   | 배송주소(주소2)                                                        | String | O  |
| appUrl             | 앱 URI                                                            | String | X  |

### 3. 계좌관리
### 4. 마이페이지