---
name: creating-java-controllers
description: Generates Spring `@RestController` classes enforcing DTO usage, service delegation, and global exception handling.
---

# Creating Java Controllers

## When to use this skill
- When exposing business logic via REST API.
- When defining HTTP endpoints.

## Principles (Strict)
1.  **@RestController Only**: Never use `@Controller` for APIs.
2.  **Service Delegation**: Controllers MUST delegate to Services. NO business logic.
3.  **No Entities**: Never accept/return `@Entity`. Use DTOs.
4.  **Error Handling**: Throw exceptions; let `@RestControllerAdvice` handle them.
5.  **Response Wrapper**: Use `ApiResponse<T>` for consistent JSON structure.

## Workflow

### 1. Define Controller
- Use `@RestController`, `@RequestMapping`, `@RequiredArgsConstructor`.
- Inject Service via constructor (final field).

### 2. Implement Endpoints
- **GET**: Return `ApiResponse<ResponseDto>`.
- **POST/PUT**: Accept `@Valid RequestDto`.
- Convert Controller DTO -> Service DTO -> Call Service -> Convert result -> Return.

### 3. Exception Handling (Global)
- Verify `GlobalExceptionHandler` exists. if not, remind user to create one.

## Template

```java
@RestController
@RequestMapping("/api/v1/users")
@RequiredArgsConstructor
@Tag(name = "User", description = "User management API")
public class UserController {

    private final UserService userService;

    @GetMapping("/{id}")
    @Operation(summary = "Get User", description = "Retrieves a user by ID")
    public ApiResponse<UserResponse> getUser(@PathVariable Long id) {
        UserDto dto = userService.getUser(id);
        return ApiResponse.success(UserResponse.of(dto));
    }

    @PostMapping
    @Operation(summary = "Create User")
    public ApiResponse<UserResponse> createUser(@Valid @RequestBody UserCreateRequest request) {
        UserDto dto = userService.createUser(request.toDto());
        return ApiResponse.created(UserResponse.of(dto));
    }
}
```

## Checklist
- [ ] Is `@RestController` used?
- [ ] Are Entities completely absent from imports?
- [ ] Is `ApiResponse` used?
- [ ] Are all inputs `@Valid`?
