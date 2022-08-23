---
description: sequence diagram
---

# 유니크로 기능 프로세스



***

### 회원가입

회원가입은 사용자가 유니크로 서비스를 이용하기 위해 반드시 선행되어야 합니다.

```html
1. 약관동의와 본인인증이 필수입니다.
2. 유니크로 화면으로 넘어와서 회원가입을 진행합니다
```

<figure><img src="https://mermaid.ink/img/pako:eNqNk89Kw0AQxl9l2JNCFet_cyhY6sGb4DWXtVm12KaaJgcRQa1CsUU9tGA1LRFaqlBBbBQPPlF39x3cNInaNZXmkmUy32--mcweoXReI0hBBXJgET1NUhm8Y-CcqoN4cNrMG9B_69JOizVv_CBzbG677Kw7lUgw26HlEj_t0gcbVjfWQYH4NPC7Cru_6b-csOYFsLsqe32GCT_InBrtuZMBSVLLwFRSgVkJJ170sg2seMqLNvB6jTU-Imip5FSEPQXmxsBB__Wl3_v0qVsGwXvDGvpeEqdA45GFhtdsqe1yi1ceR_TpWQunCJ4peWhDJXwI0bVoGgjacJDXq_TJFeD5aenD7xr86pY1XNYRZRouva5H0AOQV-B7CQR2QXLrp_n6n7zRthZDPfjrAAJCnfY_Bv6w_F1bkkDjDiiVFOLlUByacEQz7chdGmlgJZIxtEB_3QxYv35_fEZeyoFc5JzTchfFUI4YOZzRxC098pgqMndJjqhIEUeNbGMra6pI1Y9FqrWvYZOsaRlxcZGyjbMFEkPYMvObh3oaKaZhkTApuOlB1vEXR3kV3A" alt=""><figcaption><p>회원가입 프로세스</p></figcaption></figure>

### 인증

인증은 사용자 인증으로 회원가입을 제외한 API 호출시 필수로 포함되어야 합니다. 인증방식은 미정(예시로 JWT로 작성)

```html
1. 최초 API 호출 전 인증토큰을 발급받습니다.
2. 토큰의 유효시간은 2시간이며 토큰이 만료될 경우 재발급이 필요합니다
```

<figure><img src="https://mermaid.ink/img/pako:eNqNks9LAkEUx_-Vx5wKVOjXZQ5CYoc6BQVd9jK5r5LctdbdQ4gHfxDFGnhQLBthA4kOBmIRBv1F7pv_oVnUQ7ZBcxqG7_fz3nzfK7Nc0UTGWQkvPbRzmM2LU0dYhg36UCCVfKfaMJlOkwxC_0ZVh-GThO39XeCwloK9o0Og_oSe-6CuA1UdAfXaNH6FFdVr0mNL1Qarc9aSfxmZzXBYT8HMBlSvqroE9dDR9BhANpOM6YnDRjwBpuPR9O1rBjp2UJxD-Nn4oYwQWqk6cvEh8geq-fJH91H1RToQ1dVhxPjQNv8H2IzLMhzJ6eR2aRagnRAzja3U71d1P6EPSb7OoTsI79rUbc3KBI3QH7IEs9CxRN7UC1COyhjMPUMLDcb11cQT4RVcgxl2RUu9C1O4uGPm3aLD-IkolDDBhOcWD67sHOOu4-FCNF-iuaryDSF8KcU" alt=""><figcaption><p>인증 프로세스</p></figcaption></figure>

### 상품 등록

판매자가 상품을 등록합니다.

```html
1. 상품등록시 제휴사의 상품고유식별번호를 유니크로측으로 전달합니다.
2. 유니크로 상품고유식별번호를 파라미터로 넘길 시 상품수정 / 없으면 상품등록 됩니다.
3. 수정이 가능한 경우 
    3.1 해당 상품에서 발생한 거래가 없는 경우
    3.2 상품명과 가격은 수정 불가하며 변경되었을 경
```

<figure><img src="https://mermaid.ink/img/pako:eNqVVEFP4kAY_Stf5qQJNrK4uNsYEg0e9rbJXnsZ6bgSpbilPRhjsq4eGuFAdiFxSTGQaPSgCQIHTdw_xMz8h52hpZTaovTUTt573_u-93WOUaGsE6SiCvlhE6NA8kX83cQlzQDx4IJVNoHX6vT2ml3VvcPgcyWXYx2Xu0P2616FtALs7JT_doD-eaTdNrBWg_UfPE6Akxy3Q6sOP72nXRc2v34BFT7Ec2EpqMU6TToYpnyY97Xsa0f0oiXyWypklKntscaZC_xvk7WfYjTyWysxNlVYSxSBUb83Grx4WjsmwfshJH0-F34F3udIPcHhTRc2dsxcpPHqNa_dJTQWHjhIP2llTp3o5AV7Cpbs11MPFSeGHm5nxovHGg064pRV23RwTvsOv3wa9X4Cu3LoRUMM5B9r9d4f0MfAC-v2eKu2QCzZCHUmjKCNt02AlIpu8bt9jNmvJhq28lacWSUzl54UZFZZm0Pz40tITFrxSLQ-yZW1hzJFAU7J_QTmXIq9EtnSixu5tItFKwyuKzO_rS-4yGQ_xSosNN3P0y2JISfNNr06jyaWC6VQiZglXNTFHXosjzVk7ZES0ZAqXnWyi-0DS0OacSKg9qGOLbKtF8W1itRdfFAhKYRtq_ztyCgg1TJtMgH597CPOvkPH6jshg" alt=""><figcaption><p>상품 등록 프로세스</p></figcaption></figure>

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

<figure><img src="https://mermaid.ink/img/pako:eNqtlVFr01AUx7_K4T5t0AWzza7eh4GjIr4NfM1LbO60uKaaJQ8yBqvbpNA-iKy4jbRE3JyDCnWrY4KfKPfe7-C9SdrEcsPitE_N6f_8zj3_nJ67jWpNiyCMtshrj9g1Uq2bzx2zYdggPmbNbToQ_hjS81M2eB8Hp48Lq6ss8Lk_Zm-HGHQNwsuRCAA7OWSX32LxVCDFfkA7bd4a0k8-PFx_AhgWJ0lxDsyF30d0cMSCHr0al9JSkwDba_EP7fhpPqkwQ50tVF3DsKSBOAI7uRAoYP0b9qUP_F3AW6OIuOcDP-6JuIJYXVtQHB3DckGk7C-8-pVz1qyFIKF6Ppaed-nnbvGm72upf3dus5wL-aOxZw4xX2aU9Oe-eElCn-RInsjhPX86JJ1T3v1azJaytCUfPjtpIjsVy-xFTVWV2FZxM1e0ZPbu7GRFTVDYmMjiHuh1Oxzt_hcbK9F05cJvsbHyrzby40N6McbwQIP1x_JECYx3--zjgYIRJwhMJBcb5t4kM5sSRWbOqusqZXZxxb8KZbqBoqUCbHBAg7MsOq8PfWnqR_wOhXf7tDPM70S9A_XlwhzlcEqE_K9nNqcg7LLBWeHplIiyEvFX60tfUXcCc6lKVuNHN-zan79l4PSKmoZKqEGchlm3xLW1LSEGcl-QBjEQFl8tsmF6m66BDHtHSL1XlumSR1Zd3GQIb5ibW6SETM9tPn1j1xB2HY9MRMnVl6h2fgMp_7Zk" alt=""><figcaption><p>결제 프로세스</p></figcaption></figure>
