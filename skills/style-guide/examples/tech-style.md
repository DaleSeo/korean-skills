# REST API 인증 가이드 (v2.0)

## 개요

본 문서는 REST API의 OAuth 2.0 기반 인증 절차를 설명합니다.

## 사전 준비

다음 항목을 준비합니다.

- API key (관리자에게 요청)
- HTTPS 클라이언트 (curl, Postman 등)
- JSON 처리 도구 (jq 권장)

## 인증 흐름

```
1. POST /oauth/token (client_id, client_secret)
2. Receive access_token (TTL: 3600초)
3. Use Authorization: Bearer <token> for all API calls
```

## 예시 코드

```bash
curl -X POST https://api.example.com/oauth/token \
  -d "grant_type=client_credentials" \
  -d "client_id=YOUR_KEY"
```

응답:

```json
{
  "access_token": "eyJ...",
  "expires_in": 3600,
  "token_type": "Bearer"
}
```

## 에러 처리

- `401 Unauthorized`: token 만료 또는 부재
- `403 Forbidden`: 권한 부족
- `429 Too Many Requests`: 요청 한도 초과

## 변경 이력

- 2026-05-02: v2.0 출시
- 2026-04-15: v1.5 보안 패치

자세한 내용은 [API 레퍼런스](https://docs.example.com/api/v2)를 참조하세요.

---

**v1.1.0 적용 기준**: **기술 문서**

| 카테고리 | 이 글에서 적용된 기준 |
|---|---|
| 어조 | ~합니다 + 명령형 ("준비합니다") 혼용 |
| 용어 | IT 약어 OK (API, HTTPS, OAuth, TTL, JSON) |
| 숫자·단위 | 자유 (`3600초`, 코드 맥락에서 raw) |
| 목록 | `-` 부호, 인라인 코드 항목 |
| 인용 | 인라인 코드 `` `code` `` 우선 |
| 날짜 | `YYYY-MM-DD` ISO (`2026-05-02`) |
| 링크 | `[제목](URL)` 인라인 |

**일관성 평가**: ✅ 일관됨. ISO 날짜·인라인 코드·영어 약어 모두 기술 문서 표준.
