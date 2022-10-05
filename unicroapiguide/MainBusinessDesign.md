---
description: sequence diagram
---

# 유니크로 기능 프로세스

### 회원가입

제휴사 사용자가 유니크로 사용자로 회원가입합니다.

회원가입은 사용자가 유니크로 서비스를 이용하기 위해 반드시 선행되어야 합니다.

```html
1. 약관동의와 본인인증이 필수입니다.
2. 유니크로 화면으로 넘어와서 회원가입을 진행합니다.
3. DI 당 1개의 계정만 생성 가능합니다.
```

<figure><img src="https://mermaid.ink/img/pako:eNqVlM9OwkAQxl9ls2d4gR5IJPXgzcRrLwtdlEiLlvZgCAkIJkSIcpAEFAgmIppwQCnGg75Qd_sOTmlBWsq_puk22_l-33R2dvM4mZUpFnCOXhpUTVIxTU41okgqMfSsaigJqkkqgosk9ayGrOmIDV94r-FOuk_e79gdk1-PUDQWQ7zTZ7WqXRqx5w6y2w_s3URCYPaxzp8a1rjIezfIvmvxrsmHRQQDu297zBCKQ18k4DCbv5ZZBAnvtrwYV_wftCGhJfHulmzyzbuz-7W7t-WyeHdLf7H2tHTFsEJNNjEREFh_sMF6BXRwfBSkhMghCpS-KTEeyBwGdjtAvFyyy45hE-oQghLj0SAK6DuwkPU5tiY_LjKhUXLu17CvKrx5GgcLGrsZ6EVee7Hrb2v-MJhXoMhhPmtL7VZ6sW-EsDSWvofvEarK4amuNoQYX3jMe6EPVoPQFdjSBz6Ar-yreWzrzPmCziCArLDaaFt_rq1a5cOaTDdUDUewQjWFpGU48PKOjYT1M6pQCQvwKtMUMTK6hCW1AKHGhUx0eiin4dzDQopkcjSCnVPx5EpNYkHXDDoP8g5NL6rwB3bG5eA" alt=""><figcaption><p>회원가입 프로세스</p></figcaption></figure>

### 인증

인증은 사용자 인증 토큰 발급으로 회원가입을 제외한 웹 서비스 및 API 호출시 인증 토큰이 헤더에 필수로 포함되어야 합니다.&#x20;

```html
1. 최초 API 호출 전 인증토큰을 발급받습니다.
2. 토큰의 유효시간은 2시간 고정으로 연장이 되지 않습니다.
3. 토큰이 만료될 경우 재발급이 필요합니다.
```

<figure><img src="https://mermaid.ink/img/pako:eNqNks9LAkEUx_-Vx5wKVOjXZQ5CYoc6BQVd9jK5r5LctdbdQ4gHfxDFGnhQLBthA4kOBmIRBv1F7pv_oVnUQ7ZBcxqG7_fz3nzfK7Nc0UTGWQkvPbRzmM2LU0dYhg36UCCVfKfaMJlOkwxC_0ZVh-GThO39XeCwloK9o0Og_oSe-6CuA1UdAfXaNH6FFdVr0mNL1Qarc9aSfxmZzXBYT8HMBlSvqroE9dDR9BhANpOM6YnDRjwBpuPR9O1rBjp2UJxD-Nn4oYwQWqk6cvEh8geq-fJH91H1RToQ1dVhxPjQNv8H2IzLMhzJ6eR2aRagnRAzja3U71d1P6EPSb7OoTsI79rUbc3KBI3QH7IEs9CxRN7UC1COyhjMPUMLDcb11cQT4RVcgxl2RUu9C1O4uGPm3aLD-IkolDDBhOcWD67sHOOu4-FCNF-iuaryDSF8KcU" alt=""><figcaption><p>인증 프로세스</p></figcaption></figure>

### 상품 등록

제휴사 상품을 유니크로에 등록합니다.

```html
1. 상품등록시 제휴사의 상품고유식별번호를 유니크로측으로 전달합니다.
2. 제휴사에 등록된 상품을 구매자가 결제 시도 직전 유니크로 상품 등록합니다.
3. 수량은 1개로 고정입니다.
4. 결제 직전 상품이 등록되고, 등록 후 바로 결제가 되므로 상품수정은 존재하지 않습니다.
```

<figure><img src="https://mermaid.ink/img/pako:eNq9VMtOwkAU_ZXJrDSBH2gMiQQX7kzcdjO0gxLpoEO7MIREhAWGLojKQlMMGBJYYFRggQlf1Jn5B6e2PCwPUaNdNJ3Jedx7bnPzUMvqGCowh88sTDScSKMjigyVIMvMEstIYqoSIB-kmVkKhF1jnTZ_qPmX02M0FuNNRzhDftlTAC8VxXUFsJtX1moAfn_L-08-YQryCE6TVSui2GMtB-we7IPlRLA1deHNOhsMIwHMP20HwiGxsH4irsyqBcy-cEcV3pHvK3dQ5o82EHd13hgtEUvEo0uK_YZakmJ0sh7Onkd-z9wZewaSK-oO2EnSWCiSalvY3RUtzw8BKBs6foRZcsLjkVoz_sJg5qrARP_JBHzX36T-SQG4_Rd3MF4R-FtZ_isSH3D-IuGQxX_EGdbZOMWFAubD-6rnNczNup1QYAQamBoorcv1k_ckVGgeYwOrUJGfOk4hK2OqUCUFCbVOdWTiPT0ttxBUUiiTwxHo7ajDc6JBxaQWnoCCFRagCu9yeJtp" alt=""><figcaption></figcaption></figure>

### 배송 등록

판매자가 상품을 발송하고 송장번호를 입력합니다.

```html
1. 배송 등록시 거래 상태 '배송중'으로 변경된다.
2. 거래 상태 '결제완료'일 때만 배송 등록이 가능하다.
3. 배송 정보는 등록 후 수정이 불가하다
```

<figure><img src="https://mermaid.ink/img/pako:eNqlU01LAkEY_isvc7FAJSuolhASO3QLuu5l3B1Lctdadw8hQmZEoAejhIpVFIQ6GKwfhwL7Q87sf2i23fzYtKT2tDM8X-8zvDkkZWSCBJQlpwZRJRJP4UMNK6IK_MOSntHALlfoU4vVK-7l6BiKRlnDtM0-u2gLEAkDtSx21QR626HNGrDHO9Z9cTkjnMMxG7R0bRfatGnCzv4eCLA6mwtLIy_WqNJeP-jB3NOyp-3T81vEYwKshcexgRULdtEE-6HKaq8zNOKx0IyYAqzPFYFh1xr2Bq5WQiP4eAJJ3y55Xo73OI4e59hVE7YTWtQ3eKlll5_nDDZZODh5IuEffPzNc_YY7LC_tz5hTlR50Xq52IZPyhls2LFo_R4C3pO1bgLMHHwO71ZHe-fD7vvC_XOXTX9gt_YJsynpqVf5rcyt_2jP6ziy8idVFEQK0RSckvli5hwPEelHRCEiEvivTJLYSOsiEtU8hxonMtbJrpziu4qEJE5nSRBhQ88cnKkSEnTNIF8gb7k9VP4DFlgWLQ" alt=""><figcaption><p>배송 등록 프로세스</p></figcaption></figure>

### 결제

결제는 구매자가 유니크로 화면에서 PG사 화면을 호출하여 진행됩니다.

```html
1. PG사의 결제 결과는 제휴사 API를 호출하여 전달합니다.
2. PG의 처리의 실패시 제휴사에 전달하는 에러코드는 구분하여 전달합니다
```

<figure><img src="https://mermaid.ink/img/pako:eNqtVc1qwkAQfpVlTwr6AjkIFUvpTeg1l2jWVmpiG5NDEUGrgmAPpVRqSxQLSluwYNWKhT5RdvMO3WRj_Nu0UszF7Ob7mZ2dGYswnZcRFGABXRpITaNEVjrVJEVUAX0kQ8-rhpJCmrdO63kNWJ9D_NIn3Vu26S-jsRjpmbY5JddDAVjjEV0B8nRPxu8M6X91kGYPNxt2ZYifTWA_3uO3KViQGAeErI8R7rZJr4Un08jSZ7FBqhX7rsFWYc9hW3XT6yB5vG8jKrnpkogLSx1XoOoE1CKdOUcgEY9ywgxUcKK3Jt9MKKUh6XwFib9qNFKK9ziOGOXYLdO_kmbfvnkNOEfw1QQ6BKeeii1pAs8fqfLuCWX38O9s8uicVHowFjieNaxRec-pDHbYfyr9JkgeuW3p_gD7pkMe6gzu7mzIb6NWu5x99ZvI7QtAunXcG6xK8s_vx84yT4dCDTeHvx48sH__1OAWkkNfaXjKLpPuYOdC4tPXColbCovhFxA9CC0RjovdnpOZGd6cnPw6WFOCEaggTZGyMp3rRUdAhPoZUpAIBfoqo4xk5HQRimqJQo0LWdLRoZylox0KGSlXQBHoDP6TKzUNBV0z0ALk_Td4qNIPk3RgZg" alt=""><figcaption><p>결제 프로세스</p></figcaption></figure>
