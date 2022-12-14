# API

:clap: _**이 문서의 내용은 언제든지 변경될 수 있습니다.**_

### **이력**

| 개정일        | 업데이트 내용  | 작성자      |
| ---------- | -------- | -------- |
| 2022.08.18 | 초기API 세팅 | 김승희, 권희수 |

***

### **공통형식**

*   헤더

    | 파라메터              | 설명                                                                                                                                                                           |
    | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Partner-Api-Key   | <p>PARTNER_API_KEY</p><p>제휴사 구분을 위한 코드로 계약 시 발급해 드립니다.<br>웹사이트에 노출되거나 외부인에게 유출되지 않도록 주의해 주세요.</p>                                                                            |
    | Unicro-User-Token | <p>UNICRO_USER_TOKEN</p><p><a href="broken-reference/">1.1 사용자 인증 토큰 발급 API</a>를 이용해서 발급받아 사용합니다.<br><a href="broken-reference/">1. 인증 API</a> 외 모든 API 호출 시 헤더에 필수값입니다.</p> |
* 인코딩 방식
  * 유니크로 인코딩 방식은 UTF-8 형식을 사용합니다.
  * 한글이 포함된 값을 전달해주실 때에는 UTF-8 형식으로 보내주셔야 정상적인 값을 확인하실 수 있습니다.
*   응답설명

    * 응답은 json형식으로 전달합니다.

    | 파라메터    | 설명                                 |
    | ------- | ---------------------------------- |
    | result  | 성공실패 여부 코드 (성공: SUCCESS, 실패: FAIL) |
    | msg     | 응답 메시지                             |
    | errorCd | 실패시 에러 코드                          |
    | data    | 전달 Data                            |
* Content-Type
  * application/json
* 예시

```json
{
  "result": "SUCCESS",
  "msg": "토큰 발급을 성공했습니다.",
  "errorCd": "",
  "data": {
    "unicroToken": "ABCDEFG"
  }
}
```

***

### **API목록**

1. 인증 [상세API로 이동됩니다.](broken-reference)
   * 1.1. 인증 토큰 발급
2. 회원
   * 2.1 회원 등록 여부
   * 2.2 회원 탈퇴
3. 상품 (판매자) [상세API로 이동됩니다.](broken-reference)
   * 3.1. 상품 등록
4. 거래(제휴사) [상세API로 이동됩니다.](broken-reference)
   * 4.1 제휴사 거래번호로 거래조회
   * 4.2 유니크로 거래번호로 거래조회
   * 4.3 수동 배송완료 처리 (제휴사 관리자)
5. 거래 (구매자) [상세API로 이동됩니다.](broken-reference)
   * 5.1. 구매자 결제 취소
   * 5.2. 구매자 반품 요청
   * 5.3. 구매자 반품 배송정보 기입
   * 5.4. 거래 완료
   * 5.5. 구매자 거래 상세 조회
6. 거래 (판매자) [상세API로 이동됩니다.](broken-reference)
   * 6.1. 판매자 결제취소 동의
   * 6.2. 판매자 거래취소
   * 6.3. 배송정보 기입
   * 6.4. 반품 수락
   * 6.5. 반품 완료
   * 6.6. 판매자 거래 상세 조회
7. 제휴사측 개발이 필요한 부분 - 거래및 거래연관 데이터 변경 후 전달 받는 부분 [상세API로 이동됩니다.](ApiPartner.md)
   * 7.0. 유니크로 사용자 식별키 전달
   * 7.1. 제휴사 토큰 발급
   * 7.2. 결제 완료 후 성공시 전달 받을 페이지(없다면 제휴사 default 결제완료)
   * 7.3. 결제 완료 후 실패시 전달 받을 페이지(없다면 제휴사 default 결제실패)
   * 7.4. 무통장 입금완료
   * 7.5. 출금일자 전달 - 판매대금지급예정일, 판매대금지급완료일
   * 7.6. \[관리자] 거래 취소
   * 7.7. \[관리자] 택배정보 입력
   * 7.8. \[관리자] 반품택배정보 수정
   * 7.9. \[관리자] 받는사람 정보 수정(일반)
   * 7.10. \[관리자] 받는사람 정보 수정(반품)
   * 7.11. 거래상태 변경 (단건/다건)

***

### **웹 페이지**

* 제휴사에서 유니크로의 웹페이지를 호출하는 형태로 팝업창으로 제공됩니다.
