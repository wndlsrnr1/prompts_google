---
name: securing-java-endpoints
description: Implements Spring Security, JWT authentication, and method-level security.
---

# Securing Java Endpoints

## When to use this skill
- When protecting APIs.
- When configuring authentication/authorization.
- When accessing current user data.

## Principles (Strict)
1.  **JWT Only**: Stateless authentication via JWT.
2.  **Method Security**: Use `@PreAuthorize` on Controllers/Services.
3.  **AuthenticationPrincipal**: Use this to inject `ServiceUser` into Controllers.
4.  **No Logic in Config**: `SecurityConfig` should only chain filters; logic goes to Providers/Filters.

## Workflow

### 1. Security Config
Standard boilerplate for JWT filter chain.

```java
@Configuration
@EnableWebSecurity
@RequiredArgsConstructor
public class SecurityConfig {
    private final JwtAuthenticationFilter jwtFilter;

    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        return http
            .csrf(AbstractHttpConfigurer::disable)
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/api/public/**").permitAll()
                .anyRequest().authenticated()
            )
            .addFilterBefore(jwtFilter, UsernamePasswordAuthenticationFilter.class)
            .build();
    }
}
```

### 2. Method Security
Use SpEL for role checks.

```java
@PreAuthorize("hasRole('ADMIN')")
@DeleteMapping("/{id}")
public ApiResponse<Void> deleteUser(@PathVariable Long id) {
    // ...
}
```

### 3. Accessing Current User
Inject the `ServiceUser` (UserDetails implementation) directly.

```java
@GetMapping("/me")
public ApiResponse<UserDto> getMe(@AuthenticationPrincipal ServiceUser user) {
    return ApiResponse.success(userService.get(user.getId()));
}
```

## Checklist
- [ ] Is CSRF disabled (for REST)?
- [ ] Is `@AuthenticationPrincipal` used instead of looking up user from DB?
- [ ] Are public endpoints explicitly permitted?
