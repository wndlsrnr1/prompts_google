---
name: documenting-java-code
description: Enforces Swagger/OpenAPI documentation standards with bilingual descriptions.
---

# Documenting Java Code

## When to use this skill
- When creating Controllers or DTOs.
- Always required for public API artifacts.

## Principles (Strict)
1.  **Bilingual**: "Korean / English" format is MANDATORY.
2.  **Detailed Examples**: Every parameter and field must have an `example`.
3.  **RequiredMode**: Use `requiredMode = Schema.RequiredMode.REQUIRED`, NOT `required=true`.

## Workflow

### 1. Document Controller

```java
@Tag(name = "Auth", description = "인증 API / Authentication API")
public class AuthController {

    @Operation(
        summary = "로그인 / Login",
        description = "이메일과 비밀번호로 토큰을 발급받습니다. / Authenticates user and issues JWT."
    )
    @ApiResponses({
        @ApiResponse(responseCode = "200", description = "성공 / Success"),
        @ApiResponse(responseCode = "401", description = "실패 / Failed")
    })
    @PostMapping("/login")
    public ApiResponse<TokenResponse> login(...) {}
}
```

### 2. Document DTO

```java
@Schema(description = "로그인 요청 / Login Request")
public class LoginRequest {

    @Schema(
        description = "이메일 / User Email", 
        example = "user@example.com",
        requiredMode = Schema.RequiredMode.REQUIRED
    )
    private String email;
}
```

## Checklist
- [ ] Are both languages present?
- [ ] Are all `responseCode`s documented (200, 400, 401, 403, 404)?
- [ ] Do DTO fields have examples?
