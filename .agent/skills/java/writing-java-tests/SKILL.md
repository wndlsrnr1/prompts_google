---
name: writing-java-tests
description: Generates Java Unit Tests following strict TDD and Given-When-Then documentation standards.
---

# Writing Java Tests

## When to use this skill
- Before writing implementation code (TDD).
- When validating business logic in Services.
- When verifying Controller permissions/wiring.

## Principles (Strict)
1.  **Red-Green-Refactor**: Write the failing test first.
2.  **Naming Convention**: `test[MethodName]_[Scenario]`.
3.  **Target**: Primarily Service Layer (Interface based).
4.  **Documentation**: Adhere to the `Given-When-Then` Javadoc pattern requirement.

## Workflow

### 1. Service Test Template (Mockito)
Use `@ExtendWith(MockitoExtension.class)`.

```java
/**
 * Tests for {@link OrderServiceImpl}.
 * 
 * <p>
 * Test Strategy:
 * <ul>
 *   <li>Mock repositories to isolate service logic.</li>
 *   <li>Verify state transitions and exception handling.</li>
 * </ul>
 */
@ExtendWith(MockitoExtension.class)
class OrderServiceTest {

    @Mock
    private OrderRepository orderRepository;
    @Mock
    private ProductRepository productRepository;
    
    @InjectMocks
    private OrderServiceImpl orderService;

    /**
     * Tests successful order placement.
     * 
     * <p>
     * Scenario (Given-When-Then):
     * <ol>
     *   <li><strong>Given</strong>: A valid product exists with sufficient stock.</li>
     *   <li><strong>When</strong>: Order is placed.</li>
     *   <li><strong>Then</strong>: Order is saved and DTO is returned.</li>
     * </ol>
     */
    @Test
    void testPlaceOrder_Success() {
        // Given
        Product mockProduct = Product.builder().id(1L).stock(10).build();
        when(productRepository.findById(1L)).thenReturn(Optional.of(mockProduct));
        when(orderRepository.save(any(Order.class))).thenAnswer(i -> i.getArgument(0));

        // When
        OrderDto result = orderService.placeOrder(new OrderCreateDto(1L, 5));

        // Then
        assertThat(result).isNotNull();
        verify(productRepository).findById(1L);
        verify(orderRepository).save(any(Order.class));
    }
}
```

### 2. Controller Test Template (WebMvcTest)
- Focus on Status Codes and URL mapping.
- Mock the Service Interface.

## Checklist
- [ ] Does the test fail initially?
- [ ] Is the Javadoc written in English with Given/When/Then sections?
- [ ] Are strict mocks used (no actual DB connection)?
