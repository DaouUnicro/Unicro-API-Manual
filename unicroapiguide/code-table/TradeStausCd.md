# 결제 상태

| 상태                   | 상태코드 | 설명              |
| -------------------- | ---- | --------------- |
| PAY\_STANDBY         | 13   | 무통장 입금대기        |
| PAY\_APPROVED        | 31   | 결제완료            |
| DELIVERY\_ING        | 32   | 배송중             |
| DELIVERY\_DONE       | 32   | 배송완료            |
| PAY\_DONE            | 33   | 거래완료 (미입금)      |
| SETTLEMENT\_DONE     | 33   | 거래완료 (판매자 대금입금) |
| CANCEL\_REQ          | 34   | 구매자 결제취소 요청     |
| CANCEL\_DONE\_BUYER  | 35   | 구매자 요청 거래 취소    |
| CANCEL\_DONE\_SELLER | 36   | 판매자 요청 거래 취소    |
| CANCEL\_DONE\_ADMIN  | 37   | 관리자 거래 취소       |
| RETURN\_REQ          | 51   | 반품요청            |
| RETURN\_AGR          | 52   | 반품동의            |
| RETURN\_ING          | 53   | 반품배송중           |
| RETURN\_DONE         | 54   | 반품완료            |
