---
name: creating-java-services
description: Generates Java Spring Services using the Interface-Implementation pattern. Enforces strict pipeline patterns (Validation -> Logic -> Persistence).
---

# Creating Java Services

## When to use this skill
- When implementing business logic.
- When explicitly separating contract (Interface) from implementation (Class).
- When orchestrating multiple repositories.

## Principles (Strict)
1.  **Interface Design**: Follow *Effective Java Item 20*. Define `Service` interface first, then `ServiceImpl`.
2.  **Pipeline Pattern**: Every method must follow: `Validation` -> `Load` -> `Process` -> `Persist`.
3.  **DTO Input/Output**: Never accept/return Entity objects from public methods. Use Service DTOs.
4.  **Transaction Boundaries**: `@Transactional` on implementation methods (use-case level).
5.  **Repository Orchestration**: Services allow cross-repository usage. Repositories must NOT call other repositories.

## Workflow

### 1. Define Interface
Create the contract with Javadoc explaining the *business value*.

```java
public interface OrderService {
    /**
     * Processes a new order transaction.
     * @throws ServiceException if stock is insufficient
     */
    OrderDto placeOrder(OrderCreateDto request);
}
```

### 2. Implement Class
Implement the logic using the standard pipeline.

```java
@Service
@RequiredArgsConstructor
@Transactional(readOnly = true)
public class OrderServiceImpl implements OrderService {

    private final OrderRepository orderRepository;
    private final ProductRepository productRepository;
    private final UserValidator userValidator; // Component for validation

    @Override
    @Transactional
    public OrderDto placeOrder(OrderCreateDto request) {
        // 1. Validation
        userValidator.validateActive(request.getUserId());
        
        // 2. Load
        Product product = productRepository.findById(request.getProductId())
            .orElseThrow(() -> new NotFoundException("Product not found"));

        // 3. Process (Business Rules)
        product.decreaseStock(request.getQuantity()); // Domain logic inside Entity

        // 4. Persist
        Order order = Order.builder()
            .product(product)
            .quantity(request.getQuantity())
            .build();
        Order saved = orderRepository.save(order);

        // 5. Response
        return OrderDto.from(saved);
    }
}
```

### 3. Error Handling
- Use `ServiceException` or `NotFoundException` (runtime).
- Do not catch exceptions unless creating a recovery path.

## Checklist
- [ ] Is there a separate Interface and Implementation?
- [ ] Are `@Transactional` annotations correct (readOnly default vs specific)?
- [ ] Are all inputs/outputs DTOs?
- [ ] Is the pipeline (Validate->Load->Process->Save) clear?
