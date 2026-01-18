---
name: creating-java-entities

description: Generates or modifies Java Spring JPA Entities ensuring pure domain state and auditing. Use when defining new data models or updating strict domain logic.
---

# Creating Java Entities

## When to use this skill
- When creating a new database table/entity.
- When adding fields to an existing domain model.
- When defining JPA relationships (@OneToMany, @ManyToOne).

## Principles (Strict)
1.  **Pure Domain State**: Entities must only contain fields, relationships, and simple state validation.
2.  **No Business Logic**: Never put complex business rules in entities. Logic belongs in Services.
3.  **No Service Dependencies**: Entities must NEVER depend on Services or Repositories.
4.  **Auditing**: Always include `@CreatedDate` and `@LastModifiedDate`.
5.  **Access**: Use static field access over reflection.

## Workflow

### 1. Define Fields & Constraints
- Start with `@Id`, `@GeneratedValue`.
- Define columns with strict `@Column(nullable = ?, length = ?)`.
- Add `@Index` for frequently queried fields.

### 2. Define Relationships
- **Default Lazy**: `@ManyToOne(fetch = FetchType.LAZY)`.
- **Cascade Care**: Use `orphanRemoval = true` for parent-child aggregations.

### 3. Add Auditing
- Ensure the class extends a base auditing entity or includes auditing fields.

## Template

```java
package com.example.project.domain.model;

import jakarta.persistence.*;
import lombok.AccessLevel;
import lombok.Builder;
import lombok.Getter;
import lombok.NoArgsConstructor;
import org.springframework.data.annotation.CreatedDate;
import org.springframework.data.annotation.LastModifiedDate;
import org.springframework.data.jpa.domain.support.AuditingEntityListener;

import java.time.LocalDateTime;

@Entity
@Getter
@Table(name = "items", indexes = {
    @Index(name = "idx_item_code", columnList = "code")
})
@EntityListeners(AuditingEntityListener.class)
@NoArgsConstructor(access = AccessLevel.PROTECTED)
public class Item {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false, unique = true, length = 50)
    private String code;

    @Column(nullable = false)
    private String name;

    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "category_id", nullable = false)
    private Category category;

    @CreatedDate
    @Column(nullable = false, updatable = false)
    private LocalDateTime createdAt;

    @LastModifiedDate
    private LocalDateTime updatedAt;
    
    @Builder
    public Item(String code, String name, Category category) {
        this.code = code;
        this.name = name;
        this.category = category;
    }

    // Simple domain methods allowed (e.g., state updates)
    public void changeName(String newName) {
        this.name = newName;
    }
}
```

## Checklist
- [ ] Is the class annotated with `@Entity` and `@Table`?
- [ ] Are all relationships Lazy loaded by default?
- [ ] Is there a `protected` no-args constructor?
- [ ] Are auditing fields present?
- [ ] Are business rules strictly absent?
