---
name: creating-java-dtos
description: Generates Java DTOs enforcing the Two-Layer DTO pattern (Controller vs Service) and Bean Validation.
---

# Creating Java DTOs

## When to use this skill
- When defining API contracts (Request/Response).
- When passing data between Controller and Service.

## Principles (Strict)
1.  **Two-Layer Pattern**: 
    - `controller/model/*`: For HTTP (Validation, Serialization).
    - `service/model/*`: For Business Data Transfer.
    - **NEVER** mix them.
2.  **Bean Validation**: Use `@NotNull`, `@NotBlank` in Controller DTOs.
3.  **No Logic**: DTOs are data carriers. No behavior allowed except `toDto()` / `of()` converters.
4.  **Record vs Class**: Prefer `class` with `@Data` (Lombok) per project rules, but `record` is acceptable if immutable.

## Workflow

### 1. Controller DTOs (Outer Layer)
Located in `controller/{domain}/model`.

```java
@Data
public class UserCreateRequest {
    @NotBlank
    @Email
    private String email;

    @NotBlank
    private String password;

    public UserCreateRequestDto toDto() {
        return UserCreateRequestDto.builder()
            .email(this.email)
            .password(this.password)
            .build();
    }
}
```

### 2. Service DTOs (Inner Layer)
Located in `service/{domain}/model`.

```java
@Data
@Builder
public class UserDto {
    private Long id;
    private String email;
    
    public static UserDto from(User entity) {
        return UserDto.builder()
            .id(entity.getId())
            .email(entity.getEmail())
            .build();
    }
}
```

## Checklist
- [ ] Are they separated into `controller` and `service` packages?
- [ ] Do Controller DTOs have Validation annotations?
- [ ] Do Service DTOs have NO validation annotations (usually)?
- [ ] Are entities NEVER used as fields?
