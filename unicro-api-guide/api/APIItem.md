# 2. 상품(판매자)

### 2.1. 상품등록
----
판매자가 상품등록을 위해 호출하는 API입니다.

* **기능**
  상품등록

* **URI**
  /items

* **Method:**
  `POST`

*  **URL Params**

| 파라메터 | 설명 | 타입 | 필수 |
|--|--|--|--|
| partnerItemNo | 제휴사 상품번호 | String | O |
| itemName | 상품명 (200자 이하로 입력해주세요.)  | String | O |
| itemPrice | 상품가격(3000원이상 상품가격최고가격 내부 협의 필요) | String | O |
| itemCnt|판매 가능 수량(1~999) | Integer | O |
| selPayway | 결제가능한 결제수단(CARD: 신용카드, BANK: 계좌이체, VIRTUAL_ACCOUNT: 가상계좌 무통장) | String | O |
| deliveryPayType | 배송비부담 - 판매자 (CASH_ON_DELIVERY:착불, PRE_PAYMENT:선불(무료배송/택배비포함))| String | O |
| imgUrl | 이미지 경로 URI| String | X |
| aspCateNo|제휴사카테고리번호 | String | X |
| sellerUnicroUserKey | 유니크로 사용자 식별키로 유니크로 가입후 전달 한 값입니다.(판매자) | String | O |

* **응답:**
```json
{
  "result": "SUCCESS",
  "msg": "정상적으로 등록되었습니다.",
  "errorCd": "",
  "data": {
  }
}

```

| 파라메터 | 설명 |
|--|--|
| result | FAIL |
| msg | 응답 메시지  |
| errorCd | 에러코드  |
| data | 전달 Data |


| 에러코드 | 메시지 |
|--|--|
| AUTH_ERROR | 토큰 유효성 체크 실패 |
| AUTH_ERROR | 판매자인증 실패 |
| AUTH_ERROR | 판매자인증 실패 (블랙리스트) |
| AUTH_ERROR | 판매자인증 실패 (휴면상태) |
| VALID_ERROR | 필수 파라메터 없음 |
| VALID_ERROR | 상품정보오류(제휴사상품번호 20자초과) |
| VALID_ERROR | 상품정보오류(제휴사카테고리정보 20자초과) |
| VALID_ERROR | 상품정보오류(상품명 200자초과) |
| VALID_ERROR | 상품정보오류(상품가격 유효범위 초과) |
| VALID_ERROR | 상품정보오류(결제수단 오류) |
| VALID_ERROR | 상품정보오류(이미지 URI오류) |
| VALID_ERROR | 상품정보오류(판매제한 상품명 포함) |
| CREATE_ERROR | 상품등록 실패  |



### 2.2. 상품수정
----
판매자가 상품수정을 위해 호출하는 API입니다.


* **기능**
  상품수정

* **URI**
  /items/{itemNo}

* **Method:**
  `POST`

*  **URL Params**

| 파라메터 | 설명 | 타입 | 필수 |
|--|--|--|--|
| itemNo | 유니크로 상품코드 | String | X |
| partnerItemNo | 제휴사 상품번호 | String | O |
| itemName | 상품명 (200자 이하로 입력해주세요.)  | String | O |
| itemPrice | 상품가격(3000원이상 상품가격최고가격 내부 협의 필요) | String | O |
| itemCnt|판매 가능 수량(1~999) | Integer | O |
| selPayway | 결제가능한 결제수단(CARD: 신용카드, BANK: 계좌이체, VIRTUAL_ACCOUNT: 가상계좌 무통장) | String | O |
| deliveryPayType | 배송비부담 - 판매자 (CASH_ON_DELIVERY:착불, PRE_PAYMENT:선불(무료배송/택배비포함))| String | O |
| imgUrl | 이미지 경로 URI| String | X |
| aspCateNo|제휴사카테고리번호 | String | X |
| sellerUnicroUserKey | 유니크로 사용자 식별키로 유니크로 가입후 전달 한 값입니다.(판매자) | String | O |

* **응답:**
```json
{
  "result": "SUCCESS",
  "msg": "정상적으로 수정되었습니다.",
  "errorCd": "",
  "data": {
  }
}

```

| 파라메터 | 설명 |
|--|--|
| result | FAIL |
| msg | 응답 메시지  |
| errorCd | 에러코드  |
| data | 전달 Data |


| 에러코드 | 메시지 |
|--|--|
| AUTH_ERROR | 토큰 유효성 체크 실패 |
| AUTH_ERROR | 판매자인증 실패 |
| AUTH_ERROR | 판매자인증 실패 (블랙리스트) |
| AUTH_ERROR | 판매자인증 실패 (휴면상태) |
| VALID_ERROR | 필수 파라메터 없음 |
| VALID_ERROR | 상품정보오류(제휴사상품번호 20자초과) |
| VALID_ERROR | 상품정보오류(제휴사카테고리정보 20자초과) |
| VALID_ERROR | 상품정보오류(상품명 200자초과) |
| VALID_ERROR | 상품정보오류(상품가격 유효범위 초과) |
| VALID_ERROR | 상품정보오류(결제수단 오류) |
| VALID_ERROR | 상품정보오류(이미지 URI오류) |
| VALID_ERROR | 상품정보오류(판매제한 상품명 포함) |
| UPDATE_ERROR | 상품수정 실패  |



### 2.3. 상품 판매 상태 변경

----
상품 판매가능 상태를 변경하는 기능입니다.
 

* **기능**
  상품 판매가능 상태를 변경

* **URI**
  /items/{itemNo}/status

* **Method:**
  `POST`

*  **URL Params**

| 파라메터 | 설명 | 타입 | 필수 |
|--|--|--|--|
| itemNo | 유니크로 상품코드 | String | O |
| partnerItemNo | 제휴사 상품번호 | String | O |
| status| 변경하고자 하는 상태 (USE: 판매가능 , DONE: 판매완료) | String | O |
| unicroUserKey|유니크로 사용자 식별키로 유니크로 가입후 전달 한 값입니다.(판매자) | String | O |


* **응답:**
```json
{
  "result": "SUCCESS",
  "msg": "상품 상태 변경이 완료 되었습니다.",
  "errorCd": "",
  "data": {
  }
}

```


| 에러코드 | 메시지 |
|--|--|
| AUTH_ERROR | 토큰 유효성 체크 실패 |
| AUTH_ERROR | 판매자인증 실패 |
| AUTH_ERROR | 판매자인증 실패 (블랙리스트) |
| AUTH_ERROR | 판매자인증 실패 (휴면상태) |
| VALID_ERROR | 필수 파라메터 없음 |
| VALID_ERROR | 유효한 상태 변경아님 |
| UPDATE_ERROR | 상태변경 실패  |

 
