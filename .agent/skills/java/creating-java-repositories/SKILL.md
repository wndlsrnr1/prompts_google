---
name: creating-java-repositories
description: Generates Spring Data JPA Repositories and QueryDSL Custom Repositories. Enforces data access only (no logic).
---

# Creating Java Repositories

## When to use this skill
- When accessing the database.
- When complex queries (joins, dynamic filters) are needed.

## Principles (Strict)
1.  **JPA First**: Use `JpaRepository` for simple CRUD.
2.  **QueryDSL for Complex**: Use Custom Repository pattern (`QuerydslRepositorySupport`) for dynamic queries. Avoid `@Query` strings.
3.  **No Business Logic**: Repositories MUST NOT contain `if/else` business rules.
4.  **Fetch Optimization**: Use `@EntityGraph` or `fetchJoin()` to prevent N+1 problems.

## Workflow

### 1. Standard Repository
```java
@Repository
public interface UserRepository extends JpaRepository<User, Long>, CustomUserRepository {
    boolean existsByEmail(String email);
    
    @EntityGraph(attributePaths = {"roles"})
    Optional<User> findWithRolesById(Long id);
}
```

### 2. Custom Repository (QueryDSL)
Use this when you need dynamic filtering or complex joins.

**Interface:**
```java
public interface CustomUserRepository {
    List<User> search(UserSearchCondition condition);
}
```

**Implementation:**
```java
public class CustomUserRepositoryImpl extends QuerydslRepositorySupport implements CustomUserRepository {
    
    public CustomUserRepositoryImpl() {
        super(User.class);
    }

    @Override
    public List<User> search(UserSearchCondition condition) {
        return from(QUser.user)
            .where(QUser.user.age.gt(condition.getMinAge()))
            .fetch();
    }
}
```

## Checklist
- [ ] Does it extend `JpaRepository`?
- [ ] Are complex queries handled via QueryDSL?
- [ ] Is business logic absent?
