
# Examples for the Interview Traps

Short illustrative snippets. They are not full projects.

## 1. `@PathVariable` vs `@RequestParam`

```java
@RestController
@RequestMapping("/users")
public class UserController {

    // Identifies ONE resource -> path variable
    // GET /users/42
    @GetMapping("/{id}")
    public User getUser(@PathVariable Long id) {
        return userService.findById(id);
    }

    // Filters / pages a collection -> request params
    // GET /users?role=ADMIN&page=0&size=20
    @GetMapping
    public Page<User> search(
            @RequestParam(required = false) String role,
            @RequestParam(defaultValue = "0") int page,
            @RequestParam(defaultValue = "20") int size) {

        return userService.search(role, PageRequest.of(page, size));
    }
}
```

**Rule:** path = identity, params = optional filters. Never put tokens or passwords in the URL, because they end up in server logs and browser history.

## 2. `@Transactional` self-invocation

```java
@Service
public class OrderService {

    public void placeOrder(Order order) {
        save(order); // internal call bypasses Spring's proxy, so @Transactional is ignored
    }

    @Transactional
    public void save(Order order) {
        repository.save(order);
        throw new RuntimeException("fail"); // earlier save is NOT rolled back
    }
}
```

**Why:** Spring applies `@Transactional` through a proxy. A call from inside the same class never goes through the proxy.

**Fix:** move `save` into another bean and call it through that bean, so the call passes through the proxy. The same limitation applies to private and final methods.

## 3. `@Valid` vs `@Validated`

```java
public record CreateUserRequest(
    @NotBlank String name,
    @Email String email,
    @Valid @NotNull Address address   // @Valid cascades into the nested object
) {}

public record Address(@NotBlank String city) {}

@RestController
public class UserController {

    @PostMapping("/users")
    public User create(@Valid @RequestBody CreateUserRequest request) {
        return userService.create(request);
    }
}

@Service
@Validated   // enables method-level validation on this bean
public class UserService {

    public User findByEmail(@Email @NotBlank String email) {
        // Implementation omitted
    }
}
```

**Rule:** use `@Valid` (Jakarta) on request bodies and nested fields. Use `@Validated` (Spring) on service classes, or when you need validation groups.

**Exceptions:** `@Valid` on `@RequestBody` throws `MethodArgumentNotValidException`. `@Validated` on a service throws `ConstraintViolationException`.
