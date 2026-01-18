---
name: validating-java-data
description: Implements domain validation using `@Component` Validators and request validation using Bean Validation.
---

# Validating Java Data

## When to use this skill
- When validating DTO inputs (simple checks).
- When validating complex domain rules requiring DB access (e.g., "User must exist").

## Principles (Strict)
1.  **Bean Validation First**: Use annotations (`@NotNull`, `@Size`) on DTOs.
2.  **Validator Components**: For logic needing Repositories, create a `@Component`.
3.  **Fail Fast**: Validate at the TOP of the Service method.
4.  **No Logic in DTOs**: DTOs should not contain complex validation logic.

## Workflow

### 1. Bean Validation (Request DTO)
```java
public class UserCreateRequest {
    @Email(message = "Invalid email format")
    @NotBlank
    private String email;
}
```

### 2. Domain Validator Component
```java
@Component
@RequiredArgsConstructor
public class UserValidator {
    private final UserRepository userRepository;

    public void validateEmailUnique(String email) {
        if (userRepository.existsByEmail(email)) {
            throw new BusinessException(ErrorCode.EMAIL_DUPLICATED);
        }
    }
}
```

### 3. Service Usage
```java
@Service
@RequiredArgsConstructor
public class UserService {
    private final UserValidator userValidator;
    private final UserRepository userRepository;

    @Transactional
    public UserDto register(UserCreateRequest request) {
        // 1. Domain Validation
        userValidator.validateEmailUnique(request.getEmail());

        // 2. Logic
        // ...
    }
}
```

## Checklist
- [ ] Are simple checks done via annotations?
- [ ] Are complex checks isolated in a Validator class?
- [ ] Is the Validator injected into the Service?
