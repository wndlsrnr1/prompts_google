---
name: configuring-java-beans
description: Generates Spring `@Configuration` classes and manages Application Properties.
---

# Configuring Java Beans

## When to use this skill
- When defining 3rd party beans (e.g., `ObjectMapper`, `ModelMapper`).
- When binding `application.yml` properties.
- When creating profile-specific configs (`@Profile`).

## Principles (Strict)
1.  **Java Config over XML**: Always use `@Configuration` classes.
2.  **Type-Safe Properties**: Use `@ConfigurationProperties` and `@ConstructorBinding` (or `@Setter` if needed) instead of `@Value`.
3.  **Encapsulation**: Configs should be focused (e.g., `RedisConfig`, `SecurityConfig`).

## Workflow

### 1. Configuration Class
```java
@Configuration
public class JacksonConfig {
    @Bean
    public ObjectMapper objectMapper() {
        return new ObjectMapper()
            .registerModule(new JavaTimeModule())
            .disable(SerializationFeature.WRITE_DATES_AS_TIMESTAMPS);
    }
}
```

### 2. Properties Binding
```java
@Getter
@Setter
@Configuration
@ConfigurationProperties(prefix = "app.jwt")
public class JwtProperties {
    private String secret;
    private long expirationMs;
}
```

## Checklist
- [ ] Is `@Configuration` used?
- [ ] Are properties strictly typed?
- [ ] Is `@Value` avoided for complex configs?
