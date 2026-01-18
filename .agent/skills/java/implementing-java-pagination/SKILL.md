---
name: implementing-java-pagination
description: Implements Django-style pagination with `PageResponse` and strict sort field validation.
---

# Implementing Java Pagination

## When to use this skill
- When an API endpoint returns a list of items.
- When `Pageable` is needed.

## Principles (Strict)
1.  **Django Style**: Response must wrap `results`, `count`, `next`, `previous`.
2.  **Service Validation**: Services MUST validate `pageable.getSort()` fields against an allowed list to prevent SQL injection.
3.  **Pageable Binding**: Controller accepts `Pageable` directly.
4.  **Transformation**: `Page<Entity>` -> `Page<ServiceDto>` -> `PageResponse<ControllerDto>`.

## Workflow

### 1. Controller
```java
@GetMapping
public ApiResponse<PageResponse<UserResponse>> list(Pageable pageable) {
    Page<UserDto> page = userService.list(pageable);
    
    // Convert logic
    List<UserResponse> results = page.getContent().stream()
        .map(UserResponse::of)
        .toList();
        
    return ApiResponse.success(PageResponse.of(page, results));
}
```

### 2. Service
```java
private static final Set<String> ALLOWED_SORT = Set.of("id", "email", "createdAt");

public Page<UserDto> list(Pageable pageable) {
    validateSort(pageable, ALLOWED_SORT);
    
    Page<User> entityPage = userRepository.findAll(pageable);
    return entityPage.map(UserDto::from);
}

private void validateSort(Pageable pageable, Set<String> allowed) {
    if (pageable.getSort().isUnsorted()) return;
    pageable.getSort().forEach(order -> {
        if (!allowed.contains(order.getProperty())) {
             throw new BusinessException(ErrorCode.INVALID_SORT_FIELD);
        }
    });
}
```

## Checklist
- [ ] Is `PageResponse` used?
- [ ] Is Sort validation implemented in Service?
- [ ] Is `Pageable` used in Controller?
