
# Spring Boot Annotations Cheat Sheet

About 60 essential Spring Boot annotations for Java backend interviews, each with a one-word keyword, plus the traps that catch people out. Covers Spring Boot 3.x and 4.x.

**Last updated:** November 2026

## Download

- 📄 [Cheat Sheet PDF (5 slides)](Spring-Boot-Annotations-Cheat-Sheet.pdf)
- 💻 [Code examples for the traps](examples/)

![Cover](cover.png)

## What's Inside

| # | Group | Annotations |
|---|---|---|
| 01 | Core & Stereotypes | `@SpringBootApplication`, `@Component`, `@Service`, `@Repository`, `@Controller`, `@RestController`, `@Configuration`, `@Bean` |
| 02 | DI & Conditional | `@Autowired`, `@Qualifier`, `@Primary`, `@Value`, `@ConfigurationProperties`, `@Profile`, `@ConditionalOnProperty`, `@ConditionalOnMissingBean` |
| 03 | Web & Routing | `@RequestMapping`, `@GetMapping`, `@PostMapping`, `@PutMapping`, `@PatchMapping`, `@DeleteMapping` |
| 04 | Params & Payloads | `@PathVariable`, `@RequestParam`, `@RequestBody`, `@ResponseBody`, `@RequestHeader`, `@ResponseStatus` |
| 05 | Data & JPA | `@Entity`, `@Table`, `@Id`, `@GeneratedValue`, `@Column`, `@ManyToOne`, `@OneToMany`, `@JoinColumn` |
| 06 | Tx & Caching | `@Transactional`, `@EnableCaching`, `@Cacheable`, `@CacheEvict`, `@CachePut` |
| 07 | Spring Security | `@EnableWebSecurity`, `@EnableMethodSecurity`, `@PreAuthorize`, `@Secured` |
| 08 | Validation & Errors | `@Valid`, `@Validated`, `@NotNull`, `@NotEmpty`, `@NotBlank`, `@Size`, `@RestControllerAdvice` |
| 09 | Lifecycle & Testing | `@PostConstruct`, `@PreDestroy`, `@Scheduled`, `@Async`, `@SpringBootTest`, `@WebMvcTest`, `@DataJpaTest`, `@MockitoBean` |

## Interview Traps

- **`@PathVariable` vs `@RequestParam`:** Path variable identifies one resource; request params filter, sort or paginate.
- **`@Transactional` self-invocation:** Calling a `@Transactional` method from the same class skips Spring's proxy, so the annotation is ignored.
- **`@Valid` vs `@Validated`:** `@Valid` is Jakarta and cascades into nested objects; `@Validated` is Spring's and adds validation groups and method-level validation on beans.

See [examples](examples/) for code.

## Spring Boot 4 Notes

- `@MockBean` was deprecated in 3.4 and removed in 4.0. Use `@MockitoBean`.
- In Boot 4, `@SpringBootTest` no longer auto-configures MockMvc. Add `@AutoConfigureMockMvc`.
- Boot 4 also moved test annotations to new packages and modular test starters. Check the official migration guide before upgrading.

## Not All of These Are Spring Annotations

- **Jakarta Persistence:** `@Entity`, `@Table`, `@Id`, `@GeneratedValue`, `@Column`, `@ManyToOne`, `@OneToMany`, `@JoinColumn`
- **Jakarta Bean Validation:** `@Valid`, `@NotNull`, `@NotEmpty`, `@NotBlank`, `@Size`
- **Jakarta Annotations:** `@PostConstruct`, `@PreDestroy`

## How to Use This Sheet

1. Read one group at a time.
2. Cover the "meaning" column and try to recall it from the annotation name and keyword.
3. Try each trap yourself before reading the answer.

## Corrections Welcome

Found a mistake or something outdated? Open an issue. Spring changes quickly, so check the "last updated" date.

**Official docs:** https://docs.spring.io/spring-boot/

## Author

**Harsha Vardhan**

- GitHub: [Harshavardhan3535](https://github.com/Harshavardhan3535)
- LinkedIn: [Harsha Vardhan](www.linkedin.com/in/srikakulapu-harshavardhan-6367bb28b)

---

*Unofficial notes, not affiliated with the Spring project.*
