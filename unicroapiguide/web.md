# 웹

### 1. 회원가입

***

사용자의 유니크로 회원가입을 위한 유니크로 웹페이지입니다. 약관동의 > 본인인증 > 회원가입 순서로 진행됩니다.

* **기능** 회원가입
* **URI** /user/agreement
* **전달이 필요한 Params**

| 파라메터          | 설명                | 타입     | 필수 |
| ------------- | ----------------- | ------ | -- |
| partnerUserId | 제휴사 아이디           | String | O  |
| partnerApiKey | PARTNER\_API\_KEY | String | O  |

* **결과 호출** 제휴사 개발 API 7.0 유니크로 사용자 식별키 전달 호출

### 2. 결제하기

***

구매자가 상품 구매를 위한 유니크로 결제화면입니다.

* **기능** 결제하기
* **URI**
* /trades/web (웹)
* /trades/mobile (모바일)
*
* **전달이 필요한 Params**

| 파라메터            | 설명                                                               | 타입     | 필수 |
| --------------- | ---------------------------------------------------------------- | ------ | -- |
| unicroItemNo    | 유니크로 상품고유식별번호                                                    | String | O  |
| partnerTradeNo  | 제휴사 거래고유식별번호                                                     | String | O  |
| payway          | 결제수단 (CARD: 신용카드, BANK: 계좌이체, VIRTUAL\_ACCOUNT: 가상계좌 무통장)        | String | O  |
| returnUrl       | 결제 완료 후 URI                                                      | String | O  |
| deliveryPayCd   | 배송비부담 - 판매자 (CASH\_ON\_DELIVERY:착불, PRE\_PAYMENT:선불(무료배송/택배비포함)) | String | O  |
| trCodeOpt       | 현금영수증 (PERSON: 개인, BUSINESS: 사업자)                                | String | X  |
| cashInfo        | 현금영수증 > 휴대폰번호 OR 현금영수증 > 사업자번호                                   | String | X  |
| bankCd          | 은행코드 (가상계좌인 경우)                                                  | String | X  |
| unicroUserToken | UNICRO\_USER\_TOKEN                                              | String | O  |
| partnerApiKey   | PARTNER\_API\_KEY                                                | String | O  |

### 3. 계좌관리

### 4. 회원정보
