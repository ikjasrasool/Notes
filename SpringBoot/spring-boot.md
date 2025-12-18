# Complete Spring Boot Guide & Interview Questions

## Table of Contents
1. [Introduction to Spring Boot](#introduction)
2. [Core Concepts](#core-concepts)
3. [Spring Boot Architecture](#architecture)
4. [Annotations Reference](#annotations)
5. [REST API Development](#rest-api)
6. [Database Integration](#database)
7. [Security](#security)
8. [Testing](#testing)
9. [Best Practices](#best-practices)
10. [Interview Questions](#interview-questions)

---

## Introduction to Spring Boot {#introduction}

### What is Spring Boot?

Spring Boot is an open-source Java framework built on top of the Spring Framework that simplifies the development of production-ready applications. It provides:

- **Auto-configuration**: Automatically configures Spring and third-party libraries
- **Standalone**: Creates standalone applications with embedded servers
- **Opinionated defaults**: Provides sensible defaults to reduce configuration
- **Production-ready features**: Includes metrics, health checks, and externalized configuration

### Spring vs Spring Boot

| Feature | Spring | Spring Boot |
|---------|--------|-------------|
| Configuration | Extensive XML/Java configuration | Auto-configuration with minimal setup |
| Server | Requires external server (Tomcat, Jetty) | Embedded server included |
| Dependency Management | Manual dependency management | Starter dependencies |
| Setup Time | Time-consuming | Quick setup with Spring Initializr |
| Production Features | Need to configure manually | Built-in (Actuator, metrics) |

### Spring Boot Features

1. **Starter Dependencies**: Pre-configured dependency descriptors
2. **Auto-Configuration**: Automatic configuration based on classpath
3. **Embedded Servers**: Tomcat, Jetty, or Undertow
4. **Actuator**: Production-ready features (health, metrics, monitoring)
5. **Spring Boot CLI**: Command-line interface for rapid development
6. **Externalized Configuration**: Properties/YAML files
7. **DevTools**: Hot reload and automatic restart

---

## Core Concepts {#core-concepts}

### 1. Dependency Injection (DI)

Dependency Injection is a design pattern where objects receive their dependencies from external sources rather than creating them.

**Types of Dependency Injection:**

```java
// 1. Constructor Injection (Recommended)
@Service
public class ProductService {
    private final ProductRepository repository;
    
    @Autowired // Optional in Spring 4.3+
    public ProductService(ProductRepository repository) {
        this.repository = repository;
    }
}

// 2. Setter Injection
@Service
public class ProductService {
    private ProductRepository repository;
    
    @Autowired
    public void setRepository(ProductRepository repository) {
        this.repository = repository;
    }
}

// 3. Field Injection (Not recommended)
@Service
public class ProductService {
    @Autowired
    private ProductRepository repository;
}
```

**With Lombok @RequiredArgsConstructor:**

```java
@Service
@RequiredArgsConstructor
public class ProductService {
    private final ProductRepository repository;
    // Constructor automatically generated
}
```

### 2. Inversion of Control (IoC)

IoC is a principle where the control of object creation and lifecycle is transferred from the application to the Spring container.

```java
// Traditional approach (Manual control)
public class OrderService {
    private ProductRepository repository = new ProductRepository();
}

// IoC approach (Spring controls)
@Service
public class OrderService {
    private final ProductRepository repository;
    
    public OrderService(ProductRepository repository) {
        this.repository = repository; // Spring injects
    }
}
```

### 3. Spring Bean Lifecycle

```
Container Started
    ↓
Bean Instantiation
    ↓
Populate Properties (DI)
    ↓
BeanNameAware.setBeanName()
    ↓
BeanFactoryAware.setBeanFactory()
    ↓
ApplicationContextAware.setApplicationContext()
    ↓
@PostConstruct / InitializingBean.afterPropertiesSet()
    ↓
Custom init-method
    ↓
Bean Ready to Use
    ↓
@PreDestroy / DisposableBean.destroy()
    ↓
Custom destroy-method
    ↓
Container Shutdown
```

**Example:**

```java
@Component
public class LifecycleBean {
    
    @PostConstruct
    public void init() {
        System.out.println("Bean initialized");
    }
    
    @PreDestroy
    public void cleanup() {
        System.out.println("Bean destroyed");
    }
}
```

### 4. Bean Scopes

```java
// Singleton (Default) - One instance per Spring container
@Component
@Scope("singleton")
public class SingletonBean { }

// Prototype - New instance each time
@Component
@Scope("prototype")
public class PrototypeBean { }

// Request - One instance per HTTP request (Web)
@Component
@Scope("request")
public class RequestBean { }

// Session - One instance per HTTP session (Web)
@Component
@Scope("session")
public class SessionBean { }

// Application - One instance per ServletContext (Web)
@Component
@Scope("application")
public class ApplicationBean { }
```

---

## Spring Boot Architecture {#architecture}

### Layered Architecture

```
┌─────────────────────────────────────────┐
│         Presentation Layer              │
│  (Controllers, REST Endpoints)          │
│  @RestController, @Controller           │
└─────────────────┬───────────────────────┘
                  │
┌─────────────────▼───────────────────────┐
│         Service Layer                   │
│  (Business Logic)                       │
│  @Service                               │
└─────────────────┬───────────────────────┘
                  │
┌─────────────────▼───────────────────────┐
│         Repository/DAO Layer            │
│  (Data Access)                          │
│  @Repository, JpaRepository             │
└─────────────────┬───────────────────────┘
                  │
┌─────────────────▼───────────────────────┐
│         Domain/Entity Layer             │
│  (Data Models)                          │
│  @Entity                                │
└─────────────────────────────────────────┘
```

### Project Structure

```
src/main/java/com/example/project/
├── config/                 # Configuration classes
│   ├── SecurityConfig.java
│   └── DatabaseConfig.java
├── controller/             # REST controllers
│   └── ProductController.java
├── service/                # Business logic
│   ├── ProductService.java
│   └── impl/
│       └── ProductServiceImpl.java
├── repository/             # Data access
│   └── ProductRepository.java
├── entity/                 # Domain models
│   └── Product.java
├── dto/                    # Data Transfer Objects
│   ├── ProductDTO.java
│   └── ProductRequestDTO.java
├── exception/              # Custom exceptions
│   ├── ResourceNotFoundException.java
│   └── GlobalExceptionHandler.java
├── util/                   # Utility classes
│   └── DateUtil.java
└── ProjectApplication.java # Main class

src/main/resources/
├── application.properties  # Configuration
├── application-dev.properties
├── application-prod.properties
└── static/                 # Static resources
└── templates/              # Thymeleaf templates
```

---

## Annotations Reference {#annotations}

### Core Spring Annotations

```java
// Component Scanning
@Component          // Generic component
@Service           // Service layer
@Repository        // Data access layer
@Controller        // MVC controller
@RestController    // REST controller (@Controller + @ResponseBody)
@Configuration     // Configuration class

// Bean Definition
@Bean              // Method-level bean definition
@Scope             // Bean scope
@Lazy              // Lazy initialization
@Primary           // Primary bean when multiple candidates
@Qualifier         // Specify which bean to inject

// Dependency Injection
@Autowired         // Auto-wire dependencies
@Inject            // JSR-330 standard (alternative to @Autowired)
@Resource          // JSR-250 (inject by name)
@Value             // Inject property values

// Lifecycle
@PostConstruct     // Execute after DI
@PreDestroy        // Execute before destruction

// Conditional
@Conditional       // Conditional bean registration
@ConditionalOnProperty
@ConditionalOnClass
@ConditionalOnMissingBean
```

### Spring Boot Annotations

```java
@SpringBootApplication  // = @Configuration + @EnableAutoConfiguration + @ComponentScan
@EnableAutoConfiguration
@ComponentScan
@ConfigurationProperties  // Bind properties
@EnableScheduling         // Enable scheduling
@EnableAsync             // Enable async processing
@EnableCaching           // Enable caching
@EnableTransactionManagement  // Enable transactions
```

### REST Annotations

```java
@RestController    // REST endpoint
@RequestMapping    // Map requests
@GetMapping       // HTTP GET
@PostMapping      // HTTP POST
@PutMapping       // HTTP PUT
@DeleteMapping    // HTTP DELETE
@PatchMapping     // HTTP PATCH

@RequestBody      // Bind request body
@ResponseBody     // Return response body
@PathVariable     // Extract from URI
@RequestParam     // Extract query parameter
@RequestHeader    // Extract header

@ResponseStatus   // Set HTTP status
@ExceptionHandler // Handle exceptions
@ControllerAdvice // Global exception handling
```

### JPA/Hibernate Annotations

```java
@Entity           // JPA entity
@Table            // Table mapping
@Id               // Primary key
@GeneratedValue   // Auto-generation strategy
@Column           // Column mapping
@Transient        // Not persisted
@Temporal         // Date/Time mapping
@Enumerated       // Enum mapping
@Lob              // Large object

// Relationships
@OneToOne
@OneToMany
@ManyToOne
@ManyToMany
@JoinColumn
@JoinTable

// Queries
@Query            // Custom query
@NamedQuery       // Named query
@Modifying        // Modifying query
```

### Lombok Annotations

```java
@Data              // @Getter + @Setter + @ToString + @EqualsAndHashCode + @RequiredArgsConstructor
@Getter            // Generate getters
@Setter            // Generate setters
@NoArgsConstructor // No-args constructor
@AllArgsConstructor // All-args constructor
@RequiredArgsConstructor // Constructor for final fields
@ToString          // toString() method
@EqualsAndHashCode // equals() and hashCode()
@Builder           // Builder pattern
@Slf4j             // Logger field
```

### Validation Annotations

```java
@Valid             // Enable validation
@Validated         // Group validation

@NotNull           // Must not be null
@NotEmpty          // Must not be null or empty
@NotBlank          // Must not be null, empty, or whitespace
@Size              // Size constraint
@Min / @Max        // Numeric constraints
@Email             // Email format
@Pattern           // Regex pattern
@Past / @Future    // Date constraints
```

---

## REST API Development {#rest-api}

### Complete CRUD Example

#### 1. Entity Class

```java
@Entity
@Table(name = "products")
@Data
@NoArgsConstructor
@AllArgsConstructor
@Builder
public class Product {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(nullable = false)
    private String name;
    
    @Column(length = 1000)
    private String description;
    
    @Column(nullable = false)
    private Double price;
    
    private Integer quantity;
    
    @Enumerated(EnumType.STRING)
    private Category category;
    
    @CreationTimestamp
    @Column(updatable = false)
    private LocalDateTime createdAt;
    
    @UpdateTimestamp
    private LocalDateTime updatedAt;
}

enum Category {
    ELECTRONICS, CLOTHING, FOOD, BOOKS, TOYS
}
```

#### 2. DTO Classes

```java
// Request DTO
@Data
@Builder
public class ProductRequestDTO {
    @NotBlank(message = "Name is required")
    private String name;
    
    private String description;
    
    @NotNull(message = "Price is required")
    @Min(value = 0, message = "Price must be positive")
    private Double price;
    
    @Min(value = 0, message = "Quantity must be non-negative")
    private Integer quantity;
    
    @NotNull(message = "Category is required")
    private Category category;
}

// Response DTO
@Data
@Builder
public class ProductResponseDTO {
    private Long id;
    private String name;
    private String description;
    private Double price;
    private Integer quantity;
    private Category category;
    private LocalDateTime createdAt;
    private LocalDateTime updatedAt;
}
```

#### 3. Repository

```java
@Repository
public interface ProductRepository extends JpaRepository<Product, Long> {
    
    // Derived query methods
    List<Product> findByCategory(Category category);
    List<Product> findByNameContainingIgnoreCase(String name);
    List<Product> findByPriceBetween(Double minPrice, Double maxPrice);
    
    // Custom query
    @Query("SELECT p FROM Product p WHERE p.quantity < :threshold")
    List<Product> findLowStock(@Param("threshold") Integer threshold);
    
    // Native query
    @Query(value = "SELECT * FROM products WHERE price > ?1 ORDER BY price DESC", 
           nativeQuery = true)
    List<Product> findExpensiveProducts(Double price);
    
    // Check existence
    boolean existsByName(String name);
    
    // Delete operations
    void deleteByCategory(Category category);
}
```

#### 4. Service Interface

```java
public interface ProductService {
    ProductResponseDTO createProduct(ProductRequestDTO requestDTO);
    ProductResponseDTO getProductById(Long id);
    List<ProductResponseDTO> getAllProducts();
    ProductResponseDTO updateProduct(Long id, ProductRequestDTO requestDTO);
    void deleteProduct(Long id);
    List<ProductResponseDTO> getProductsByCategory(Category category);
    List<ProductResponseDTO> searchProducts(String keyword);
}
```

#### 5. Service Implementation

```java
@Service
@RequiredArgsConstructor
@Slf4j
public class ProductServiceImpl implements ProductService {
    
    private final ProductRepository productRepository;
    
    @Override
    public ProductResponseDTO createProduct(ProductRequestDTO requestDTO) {
        log.info("Creating product: {}", requestDTO.getName());
        
        // Check if product already exists
        if (productRepository.existsByName(requestDTO.getName())) {
            throw new DuplicateResourceException("Product with name already exists");
        }
        
        Product product = Product.builder()
            .name(requestDTO.getName())
            .description(requestDTO.getDescription())
            .price(requestDTO.getPrice())
            .quantity(requestDTO.getQuantity())
            .category(requestDTO.getCategory())
            .build();
            
        Product savedProduct = productRepository.save(product);
        return mapToResponseDTO(savedProduct);
    }
    
    @Override
    public ProductResponseDTO getProductById(Long id) {
        log.info("Fetching product with id: {}", id);
        
        Product product = productRepository.findById(id)
            .orElseThrow(() -> new ResourceNotFoundException("Product not found with id: " + id));
            
        return mapToResponseDTO(product);
    }
    
    @Override
    public List<ProductResponseDTO> getAllProducts() {
        log.info("Fetching all products");
        
        return productRepository.findAll().stream()
            .map(this::mapToResponseDTO)
            .collect(Collectors.toList());
    }
    
    @Override
    @Transactional
    public ProductResponseDTO updateProduct(Long id, ProductRequestDTO requestDTO) {
        log.info("Updating product with id: {}", id);
        
        Product existingProduct = productRepository.findById(id)
            .orElseThrow(() -> new ResourceNotFoundException("Product not found with id: " + id));
        
        existingProduct.setName(requestDTO.getName());
        existingProduct.setDescription(requestDTO.getDescription());
        existingProduct.setPrice(requestDTO.getPrice());
        existingProduct.setQuantity(requestDTO.getQuantity());
        existingProduct.setCategory(requestDTO.getCategory());
        
        Product updatedProduct = productRepository.save(existingProduct);
        return mapToResponseDTO(updatedProduct);
    }
    
    @Override
    public void deleteProduct(Long id) {
        log.info("Deleting product with id: {}", id);
        
        if (!productRepository.existsById(id)) {
            throw new ResourceNotFoundException("Product not found with id: " + id);
        }
        
        productRepository.deleteById(id);
    }
    
    @Override
    public List<ProductResponseDTO> getProductsByCategory(Category category) {
        return productRepository.findByCategory(category).stream()
            .map(this::mapToResponseDTO)
            .collect(Collectors.toList());
    }
    
    @Override
    public List<ProductResponseDTO> searchProducts(String keyword) {
        return productRepository.findByNameContainingIgnoreCase(keyword).stream()
            .map(this::mapToResponseDTO)
            .collect(Collectors.toList());
    }
    
    // Helper method to map Entity to DTO
    private ProductResponseDTO mapToResponseDTO(Product product) {
        return ProductResponseDTO.builder()
            .id(product.getId())
            .name(product.getName())
            .description(product.getDescription())
            .price(product.getPrice())
            .quantity(product.getQuantity())
            .category(product.getCategory())
            .createdAt(product.getCreatedAt())
            .updatedAt(product.getUpdatedAt())
            .build();
    }
}
```

#### 6. Controller

```java
@RestController
@RequestMapping("/api/products")
@RequiredArgsConstructor
@Slf4j
public class ProductController {
    
    private final ProductService productService;
    
    @PostMapping
    @ResponseStatus(HttpStatus.CREATED)
    public ResponseEntity<ApiResponse<ProductResponseDTO>> createProduct(
            @Valid @RequestBody ProductRequestDTO requestDTO) {
        
        log.info("REST request to create product: {}", requestDTO.getName());
        
        ProductResponseDTO response = productService.createProduct(requestDTO);
        
        return ResponseEntity
            .status(HttpStatus.CREATED)
            .body(new ApiResponse<>(true, "Product created successfully", response));
    }
    
    @GetMapping("/{id}")
    public ResponseEntity<ApiResponse<ProductResponseDTO>> getProductById(@PathVariable Long id) {
        log.info("REST request to get product: {}", id);
        
        ProductResponseDTO response = productService.getProductById(id);
        
        return ResponseEntity.ok(
            new ApiResponse<>(true, "Product retrieved successfully", response)
        );
    }
    
    @GetMapping
    public ResponseEntity<ApiResponse<List<ProductResponseDTO>>> getAllProducts() {
        log.info("REST request to get all products");
        
        List<ProductResponseDTO> response = productService.getAllProducts();
        
        return ResponseEntity.ok(
            new ApiResponse<>(true, "Products retrieved successfully", response)
        );
    }
    
    @PutMapping("/{id}")
    public ResponseEntity<ApiResponse<ProductResponseDTO>> updateProduct(
            @PathVariable Long id,
            @Valid @RequestBody ProductRequestDTO requestDTO) {
        
        log.info("REST request to update product: {}", id);
        
        ProductResponseDTO response = productService.updateProduct(id, requestDTO);
        
        return ResponseEntity.ok(
            new ApiResponse<>(true, "Product updated successfully", response)
        );
    }
    
    @DeleteMapping("/{id}")
    public ResponseEntity<ApiResponse<Void>> deleteProduct(@PathVariable Long id) {
        log.info("REST request to delete product: {}", id);
        
        productService.deleteProduct(id);
        
        return ResponseEntity.ok(
            new ApiResponse<>(true, "Product deleted successfully", null)
        );
    }
    
    @GetMapping("/category/{category}")
    public ResponseEntity<ApiResponse<List<ProductResponseDTO>>> getProductsByCategory(
            @PathVariable Category category) {
        
        log.info("REST request to get products by category: {}", category);
        
        List<ProductResponseDTO> response = productService.getProductsByCategory(category);
        
        return ResponseEntity.ok(
            new ApiResponse<>(true, "Products retrieved successfully", response)
        );
    }
    
    @GetMapping("/search")
    public ResponseEntity<ApiResponse<List<ProductResponseDTO>>> searchProducts(
            @RequestParam String keyword) {
        
        log.info("REST request to search products with keyword: {}", keyword);
        
        List<ProductResponseDTO> response = productService.searchProducts(keyword);
        
        return ResponseEntity.ok(
            new ApiResponse<>(true, "Products retrieved successfully", response)
        );
    }
}
```

#### 7. Generic API Response

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class ApiResponse<T> {
    private boolean success;
    private String message;
    private T data;
}
```

#### 8. Exception Handling

```java
// Custom Exceptions
public class ResourceNotFoundException extends RuntimeException {
    public ResourceNotFoundException(String message) {
        super(message);
    }
}

public class DuplicateResourceException extends RuntimeException {
    public DuplicateResourceException(String message) {
        super(message);
    }
}

// Global Exception Handler
@RestControllerAdvice
@Slf4j
public class GlobalExceptionHandler {
    
    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<ErrorResponse> handleResourceNotFound(ResourceNotFoundException ex) {
        log.error("Resource not found: {}", ex.getMessage());
        
        ErrorResponse error = new ErrorResponse(
            HttpStatus.NOT_FOUND.value(),
            ex.getMessage(),
            LocalDateTime.now()
        );
        
        return new ResponseEntity<>(error, HttpStatus.NOT_FOUND);
    }
    
    @ExceptionHandler(DuplicateResourceException.class)
    public ResponseEntity<ErrorResponse> handleDuplicateResource(DuplicateResourceException ex) {
        log.error("Duplicate resource: {}", ex.getMessage());
        
        ErrorResponse error = new ErrorResponse(
            HttpStatus.CONFLICT.value(),
            ex.getMessage(),
            LocalDateTime.now()
        );
        
        return new ResponseEntity<>(error, HttpStatus.CONFLICT);
    }
    
    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<ErrorResponse> handleValidationErrors(MethodArgumentNotValidException ex) {
        log.error("Validation error: {}", ex.getMessage());
        
        Map<String, String> errors = new HashMap<>();
        ex.getBindingResult().getFieldErrors().forEach(error -> 
            errors.put(error.getField(), error.getDefaultMessage())
        );
        
        ErrorResponse error = new ErrorResponse(
            HttpStatus.BAD_REQUEST.value(),
            "Validation failed",
            LocalDateTime.now(),
            errors
        );
        
        return new ResponseEntity<>(error, HttpStatus.BAD_REQUEST);
    }
    
    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleGenericException(Exception ex) {
        log.error("Internal server error: {}", ex.getMessage(), ex);
        
        ErrorResponse error = new ErrorResponse(
            HttpStatus.INTERNAL_SERVER_ERROR.value(),
            "An unexpected error occurred",
            LocalDateTime.now()
        );
        
        return new ResponseEntity<>(error, HttpStatus.INTERNAL_SERVER_ERROR);
    }
}

@Data
@AllArgsConstructor
@NoArgsConstructor
class ErrorResponse {
    private int status;
    private String message;
    private LocalDateTime timestamp;
    private Map<String, String> errors;
    
    public ErrorResponse(int status, String message, LocalDateTime timestamp) {
        this.status = status;
        this.message = message;
        this.timestamp = timestamp;
    }
}
```

---

## Database Integration {#database}

### application.properties Configuration

```properties
# Database Configuration
spring.datasource.url=jdbc:mysql://localhost:3306/productdb?createDatabaseIfNotExist=true
spring.datasource.username=root
spring.datasource.password=password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# JPA/Hibernate Properties
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect
spring.jpa.open-in-view=false

# Connection Pool (HikariCP - Default in Spring Boot)
spring.datasource.hikari.maximum-pool-size=10
spring.datasource.hikari.minimum-idle=5
spring.datasource.hikari.connection-timeout=30000

# Logging
logging.level.org.hibernate.SQL=DEBUG
logging.level.org.hibernate.type.descriptor.sql.BasicBinder=TRACE

# Server Configuration
server.port=8080
server.error.include-message=always
server.error.include-stacktrace=on_param
```

### Multiple Databases Configuration

```java
@Configuration
@EnableTransactionManagement
@EnableJpaRepositories(
    basePackages = "com.example.repository.primary",
    entityManagerFactoryRef = "primaryEntityManagerFactory",
    transactionManagerRef = "primaryTransactionManager"
)
public class PrimaryDataSourceConfig {
    
    @Primary
    @Bean
    @ConfigurationProperties(prefix = "spring.datasource.primary")
    public DataSource primaryDataSource() {
        return DataSourceBuilder.create().build();
    }
    
    @Primary
    @Bean
    public LocalContainerEntityManagerFactoryBean primaryEntityManagerFactory(
            EntityManagerFactoryBuilder builder,
            @Qualifier("primaryDataSource") DataSource dataSource) {
        return builder
            .dataSource(dataSource)
            .packages("com.example.entity.primary")
            .persistenceUnit("primary")
            .build();
    }
    
    @Primary
    @Bean
    public PlatformTransactionManager primaryTransactionManager(
            @Qualifier("primaryEntityManagerFactory") EntityManagerFactory entityManagerFactory) {
        return new JpaTransactionManager(entityManagerFactory);
    }
}
```

### Entity Relationships

```java
// One-to-One
@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @OneToOne(cascade = CascadeType.ALL, fetch = FetchType.LAZY)
    @JoinColumn(name = "profile_id", referencedColumnName = "id")
    private UserProfile profile;
}

@Entity
public class UserProfile {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @OneToOne(mappedBy = "profile")
    private User user;
}

// One-to-Many / Many-to-One
@Entity
public class Department {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @OneToMany(mappedBy = "department", cascade = CascadeType.ALL, fetch = FetchType.LAZY)
    private List<Employee> employees = new ArrayList<>();
}

@Entity
public class Employee {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "department_id")
    private Department department;
}

// Many-to-Many
@Entity
public class Student {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @ManyToMany(cascade = {CascadeType.PERSIST, CascadeType.MERGE})
    @JoinTable(
        name = "student_course",
        joinColumns = @JoinColumn(name = "student_id"),
        inverseJoinColumns = @JoinColumn(name = "course_id")
    )
    private Set<Course> courses = new HashSet<>();
}

@Entity
public class Course {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @ManyToMany(mappedBy = "courses")
    private Set<Student> students = new HashSet<>();
}
```

---

## Security {#security}

### Spring Security Configuration

```java
@Configuration
@EnableWebSecurity
@RequiredArgsConstructor
public class SecurityConfig {
    
    private final UserDetailsService userDetailsService;
    private final JwtAuthenticationFilter jwtAuthFilter;
    
    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .csrf(csrf -> csrf.disable())
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/api/auth/**", "/api/public/**").permitAll()
                .requestMatchers("/api/admin/**").hasRole("ADMIN")
                .requestMatchers("/api/user/**").hasAnyRole("USER", "ADMIN")
                .anyRequest().authenticated()
            )
            .sessionManagement(session -> session
                .sessionCreationPolicy(SessionCreationPolicy.STATELESS)
            )
            .authenticationProvider(authenticationProvider())
            .addFilterBefore(jwtAuthFilter, UsernamePasswordAuthenticationFilter.class);
        
        return http.build();
    }
    
    @Bean
    public AuthenticationProvider authenticationProvider() {
        DaoAuthenticationProvider authProvider = new DaoAuthenticationProvider();
        authProvider.setUserDetailsService(userDetailsService);
        authProvider.setPasswordEncoder(passwordEncoder());
        return authProvider;
    }
    
    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
    
    @Bean
    public AuthenticationManager authenticationManager(AuthenticationConfiguration config) 
            throws Exception {
        return config.getAuthenticationManager();
    }
}
```

### JWT Implementation

```java
@Component
public class JwtService {
    
    @Value("${jwt.secret}")
    private String secretKey;
    
    @Value("${jwt.expiration}")
    private long jwtExpiration;
    
    public String extractUsername(String token) {
        return extractClaim(token, Claims::getSubject);
    }
    
    public <T> T extractClaim(String token, Function<Claims, T> claimsResolver) {
        final Claims claims = extractAllClaims(token);
        return claimsResolver.apply(claims);
    }
    
    public String generateToken(UserDetails userDetails) {
        return generateToken(new HashMap<>(), userDetails);
    }
    
    public String generateToken(Map<String, Object> extraClaims, UserDetails userDetails) {
        return Jwts
            .builder()
            .setClaims(extraClaims)
            .setSubject(userDetails.getUsername())
            .setIssuedAt(new Date(System.currentTimeMillis()))
            .setExpiration(new Date(System.currentTimeMillis() + jwtExpiration))
            .signWith(getSignInKey(), SignatureAlgorithm.HS256)
            .compact();
    }
    
    public boolean isTokenValid(String token, UserDetails userDetails) {
        final String username = extractUsername(token);
        return (username.equals(userDetails.getUsername())) && !isTokenExpired(token);
    }
    
    private boolean isTokenExpired(String token) {
        return extractExpiration(token).before(new Date());
    }
    
    private Date extractExpiration(String token) {
        return extractClaim(token, Claims::getExpiration);
    }
    
    private Claims extractAllClaims(String token) {
        return Jwts
            .parserBuilder()
            .setSigningKey(getSignInKey())
            .build()
            .parseClaimsJws(token)
            .getBody();
    }
    
    private Key getSignInKey() {
        byte[] keyBytes = Decoders.BASE64.decode(secretKey);
        return Keys.hmacShaKeyFor(keyBytes);
    }
}
```

---

## Testing {#testing}

### Unit Testing with JUnit and Mockito

```java
@ExtendWith(MockitoExtension.class)
class ProductServiceTest {
    
    @Mock
    private ProductRepository productRepository;
    
    @InjectMocks
    private ProductServiceImpl productService;
    
    private Product product;
    private ProductRequestDTO requestDTO;
    
    @BeforeEach
    void setUp() {
        product = Product.builder()
            .id(1L)
            .name("Test Product")
            .description("Test Description")
            .price(99.99)
            .quantity(10)
            .category(Category.ELECTRONICS)
            .build();
        
        requestDTO = ProductRequestDTO.builder()
            .name("Test Product")
            .description("Test Description")
            .price(99.99)
            .quantity(10)
            .category(Category.ELECTRONICS)
            .build();
    }
    
    @Test
    void testCreateProduct_Success() {
        // Arrange
        when(productRepository.existsByName(anyString())).thenReturn(false);
        when(productRepository.save(any(Product.class))).thenReturn(product);
        
        // Act
        ProductResponseDTO response = productService.createProduct(requestDTO);
        
        // Assert
        assertNotNull(response);
        assertEquals("Test Product", response.getName());
        verify(productRepository, times(1)).save(any(Product.class));
    }
    
    @Test
    void testGetProductById_NotFound() {
        // Arrange
        when(productRepository.findById(anyLong())).thenReturn(Optional.empty());
        
        // Act & Assert
        assertThrows(ResourceNotFoundException.class, 
            () -> productService.getProductById(1L));
    }
    
    @Test
    void testGetAllProducts_Success() {
        // Arrange
        List<Product> products = Arrays.asList(product);
        when(productRepository.findAll()).thenReturn(products);
        
        // Act
        List<ProductResponseDTO> response = productService.getAllProducts();
        
        // Assert
        assertEquals(1, response.size());
        verify(productRepository, times(1)).findAll();
    }
}
```

### Integration Testing

```java
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
@AutoConfigureMockMvc
@Transactional
class ProductControllerIntegrationTest {
    
    @Autowired
    private MockMvc mockMvc;
    
    @Autowired
    private ObjectMapper objectMapper;
    
    @Autowired
    private ProductRepository productRepository;
    
    @BeforeEach
    void setUp() {
        productRepository.deleteAll();
    }
    
    @Test
    void testCreateProduct_Success() throws Exception {
        ProductRequestDTO request = ProductRequestDTO.builder()
            .name("Integration Test Product")
            .description("Test Description")
            .price(49.99)
            .quantity(5)
            .category(Category.BOOKS)
            .build();
        
        mockMvc.perform(post("/api/products")
                .contentType(MediaType.APPLICATION_JSON)
                .content(objectMapper.writeValueAsString(request)))
            .andExpect(status().isCreated())
            .andExpect(jsonPath("$.success").value(true))
            .andExpect(jsonPath("$.data.name").value("Integration Test Product"))
            .andExpect(jsonPath("$.data.price").value(49.99));
    }
    
    @Test
    void testGetProductById_NotFound() throws Exception {
        mockMvc.perform(get("/api/products/999"))
            .andExpect(status().isNotFound());
    }
}
```

### Repository Testing

```java
@DataJpaTest
@AutoConfigureTestDatabase(replace = AutoConfigureTestDatabase.Replace.NONE)
class ProductRepositoryTest {
    
    @Autowired
    private ProductRepository productRepository;
    
    @Test
    void testFindByCategory_Success() {
        // Arrange
        Product product = Product.builder()
            .name("Test Product")
            .price(29.99)
            .category(Category.ELECTRONICS)
            .build();
        productRepository.save(product);
        
        // Act
        List<Product> products = productRepository.findByCategory(Category.ELECTRONICS);
        
        // Assert
        assertEquals(1, products.size());
        assertEquals("Test Product", products.get(0).getName());
    }
}
```

---

## Best Practices {#best-practices}

### 1. Use Constructor Injection

```java
// Good - Constructor Injection
@Service
@RequiredArgsConstructor
public class ProductService {
    private final ProductRepository repository;
}

// Avoid - Field Injection
@Service
public class ProductService {
    @Autowired
    private ProductRepository repository;
}
```

### 2. Use DTOs for API Communication

```java
// Don't expose entities directly
@GetMapping
public List<ProductDTO> getProducts() {
    return service.getAllProducts();
}

// Use mapper utilities
private ProductDTO toDTO(Product entity) {
    return mapper.map(entity, ProductDTO.class);
}
```

### 3. Implement Proper Exception Handling

```java
@RestControllerAdvice
public class GlobalExceptionHandler {
    
    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<ErrorResponse> handleNotFound(ResourceNotFoundException ex) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND)
            .body(new ErrorResponse(ex.getMessage()));
    }
}
```

### 4. Use Validation

```java
@PostMapping
public ResponseEntity<Product> create(@Valid @RequestBody ProductDTO dto) {
    return ResponseEntity.ok(service.create(dto));
}
```

### 5. Profile-based Configuration

```properties
# application-dev.properties
spring.jpa.show-sql=true
logging.level.root=DEBUG

# application-prod.properties
spring.jpa.show-sql=false
logging.level.root=WARN
```

### 6. Use Lombok Wisely

```java
@Data // Use for DTOs
@Builder // Use for object creation
@RequiredArgsConstructor // Use for DI
@Slf4j // Use for logging
```

### 7. Implement Pagination

```java
@GetMapping
public Page<ProductDTO> getProducts(
    @RequestParam(defaultValue = "0") int page,
    @RequestParam(defaultValue = "10") int size,
    @RequestParam(defaultValue = "id") String sortBy) {
    
    Pageable pageable = PageRequest.of(page, size, Sort.by(sortBy));
    return service.getAllProducts(pageable);
}
```

### 8. Use Transactions Properly

```java
@Transactional
public void transferMoney(Long from, Long to, Double amount) {
    accountService.debit(from, amount);
    accountService.credit(to, amount);
}
```

---

## Interview Questions {#interview-questions}

### Basic Questions

**Q1: What is Spring Boot and why use it?**

Spring Boot is a framework that simplifies Spring application development by providing auto-configuration, embedded servers, and production-ready features. It eliminates boilerplate configuration and allows rapid application development.

**Q2: What is the difference between @Component, @Service, and @Repository?**

- `@Component`: Generic stereotype for any Spring-managed component
- `@Service`: Specialization for service layer (business logic)
- `@Repository`: Specialization for persistence layer (data access), provides exception translation

**Q3: Explain Dependency Injection.**

DI is a design pattern where objects receive dependencies from external sources rather than creating them. Spring IoC container injects dependencies via constructor, setter, or field injection.

**Q4: What is @SpringBootApplication?**

It's a meta-annotation combining:
- `@Configuration`: Marks class as configuration source
- `@EnableAutoConfiguration`: Enables auto-configuration
- `@ComponentScan`: Enables component scanning

**Q5: What are Spring Boot Starters?**

Pre-configured dependency descriptors that simplify dependency management. Examples:
- `spring-boot-starter-web`: Web applications
- `spring-boot-starter-data-jpa`: JPA with Hibernate
- `spring-boot-starter-security`: Security features

### Intermediate Questions

**Q6: Explain different types of Dependency Injection.**

1. **Constructor Injection** (recommended): Dependencies via constructor
2. **Setter Injection**: Dependencies via setter methods
3. **Field Injection**: Direct field injection (not recommended)

**Q7: What is the difference between @Autowired and @Inject?**

- `@Autowired`: Spring-specific annotation
- `@Inject`: JSR-330 standard, more portable
Both perform dependency injection, `@Autowired` has more features (required attribute)

**Q8: Explain Bean Scopes.**

- **Singleton**: One instance per container (default)
- **Prototype**: New instance per request
- **Request**: One instance per HTTP request
- **Session**: One instance per HTTP session
- **Application**: One instance per ServletContext

**Q9: What is Spring Boot Actuator?**

Production-ready features for monitoring and managing applications:
- Health checks (`/actuator/health`)
- Metrics (`/actuator/metrics`)
- Environment info (`/actuator/env`)
- Application info (`/actuator/info`)

**Q10: How does Spring Boot Auto-configuration work?**

Spring Boot uses `@EnableAutoConfiguration` to automatically configure beans based on:
- Classpath dependencies
- Existing beans
- Property settings
Uses `@Conditional` annotations to determine what to configure.

### Advanced Questions

**Q11: Explain the difference between @RestController and @Controller.**

- `@Controller`: Returns view name for MVC applications
- `@RestController`: Combination of `@Controller` + `@ResponseBody`, returns data directly (JSON/XML)

**Q12: What is the difference between JPA and Hibernate?**

- **JPA**: Specification/Interface for ORM (Java Persistence API)
- **Hibernate**: Implementation of JPA specification (also has additional features)

**Q13: Explain transaction management in Spring.**

Spring provides declarative transaction management via `@Transactional`:
- Programmatic: Using `TransactionTemplate`
- Declarative: Using `@Transactional` annotation
Supports propagation, isolation levels, rollback rules.

**Q14: How to handle exceptions globally in Spring Boot?**

Use `@RestControllerAdvice` with `@ExceptionHandler`:
```java
@RestControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<Error> handle(ResourceNotFoundException ex) {
        return ResponseEntity.status(404).body(new Error(ex.getMessage()));
    }
}
```

**Q15: What is the N+1 query problem and how to solve it?**

**Problem**: Executing 1 query for parent + N queries for children

**Solutions**:
- Use `@EntityGraph`
- Use `JOIN FETCH` in JPQL
- Set `FetchType.LAZY` appropriately
- Use batch fetching

**Q16: Explain Spring Security Architecture.**

Key components:
- **SecurityContext**: Holds security information
- **Authentication**: Principal identity
- **AuthenticationManager**: Authenticates users
- **UserDetailsService**: Loads user data
- **GrantedAuthority**: Permissions/roles
- **SecurityFilterChain**: Filter chain for requests

**Q17: What is the difference between @PathVariable and @RequestParam?**

```java
// @PathVariable - Extract from URI path
@GetMapping("/products/{id}")
public Product get(@PathVariable Long id) { }
// URL: /products/123

// @RequestParam - Extract query parameter
@GetMapping("/products")
public List<Product> search(@RequestParam String name) { }
// URL: /products?name=laptop
```

**Q18: How to implement caching in Spring Boot?**

```java
@Configuration
@EnableCaching
public class CacheConfig { }

@Service
public class ProductService {
    @Cacheable("products")
    public Product getById(Long id) { }
    
    @CacheEvict(value = "products", allEntries = true)
    public void clearCache() { }
}
```

**Q19: What is the difference between application.properties and application.yml?**

Both configure Spring Boot applications:
- **properties**: Key-value format
- **yml**: Hierarchical YAML format (more readable for complex configs)

**Q20: How to implement pagination and sorting?**

```java
@GetMapping
public Page<Product> getAll(
    @PageableDefault(size = 20, sort = "id") Pageable pageable) {
    return repository.findAll(pageable);
}
```

### Scenario-Based Questions

**Q21: How would you handle circular dependencies?**

Solutions:
1. Use `@Lazy` annotation
2. Use setter injection instead of constructor
3. Redesign code to eliminate circular dependency
4. Use `@PostConstruct` for initialization

**Q22: How to optimize database queries?**

- Use pagination for large datasets
- Implement caching strategically
- Use lazy loading for associations
- Create appropriate database indexes
- Use projection DTOs to fetch only needed fields
- Use batch operations for bulk updates
- Monitor and analyze query performance

**Q23: How to implement API versioning?**

Methods:
1. **URI versioning**: `/api/v1/products`
2. **Request parameter**: `/api/products?version=1`
3. **Header versioning**: `X-API-Version: 1`
4. **Media type versioning**: `Accept: application/vnd.api.v1+json`

**Q24: How to secure REST APIs?**

- Implement authentication (JWT, OAuth2)
- Use HTTPS for all communications
- Validate and sanitize inputs
- Implement rate limiting
- Use CORS properly
- Implement role-based access control
- Log security events
- Keep dependencies updated

**Q25: How to handle file uploads?**

```java
@PostMapping("/upload")
public ResponseEntity<String> upload(
    @RequestParam("file") MultipartFile file) {
    
    if (file.isEmpty()) {
        return ResponseEntity.badRequest()
            .body("File is empty");
    }
    
    // Save file logic
    String filename = file.getOriginalFilename();
    Path path = Paths.get(uploadDir + filename);
    Files.copy(file.getInputStream(), path);
    
    return ResponseEntity.ok("Uploaded: " + filename);
}
```

### Additional Important Topics

**Q26: What is Spring Boot DevTools?**

Development-time tools providing:
- Automatic restart on code changes
- LiveReload browser plugin support
- Property defaults for development
- Enhanced error pages

**Q27: How to externalize configuration?**

Multiple sources (priority order):
1. Command-line arguments
2. Java System properties
3. OS environment variables
4. `application.properties`/`application.yml`
5. `@PropertySource` annotations

**Q28: What is @Transactional propagation?**

Controls transaction behavior:
- **REQUIRED**: Use existing or create new (default)
- **REQUIRES_NEW**: Always create new transaction
- **NESTED**: Execute within nested transaction
- **MANDATORY**: Must run within existing transaction
- **SUPPORTS**: Use transaction if exists
- **NOT_SUPPORTED**: Execute non-transactionally
- **NEVER**: Throw exception if transaction exists

**Q29: Explain lazy vs eager loading.**

- **Lazy Loading** (`FetchType.LAZY`): Load data when accessed (better performance)
- **Eager Loading** (`FetchType.EAGER`): Load data immediately (may cause performance issues)

**Q30: How to implement async processing?**

```java
@Configuration
@EnableAsync
public class AsyncConfig {
    @Bean
    public Executor taskExecutor() {
        ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
        executor.setCorePoolSize(5);
        executor.setMaxPoolSize(10);
        executor.setQueueCapacity(100);
        executor.initialize();
        return executor;
    }
}

@Service
public class EmailService {
    @Async
    public CompletableFuture<String> sendEmail(String to) {
        // Send email logic
        return CompletableFuture.completedFuture("Sent");
    }
}
```

---

## Useful Resources

### Official Documentation
- Spring Boot Documentation: https://spring.io/projects/spring-boot
- Spring Data JPA: https://spring.io/projects/spring-data-jpa
- Spring Security: https://spring.io/projects/spring-security

### Tools
- Spring Initializr: https://start.spring.io/
- Postman: API testing
- MySQL Workbench: Database management
- IntelliJ IDEA / VS Code: IDEs

### Best Practice Checklist
✅ Use constructor injection with `@RequiredArgsConstructor`  
✅ Implement DTOs for API layer  
✅ Add proper validation with Bean Validation  
✅ Implement global exception handling  
✅ Use proper HTTP status codes  
✅ Document APIs (Swagger/OpenAPI)  
✅ Write unit and integration tests  
✅ Use pagination for large datasets  
✅ Implement proper logging  
✅ Secure sensitive endpoints  
✅ Use profiles for different environments  
✅ Follow RESTful conventions  
✅ Implement proper transaction management  
✅ Use caching where appropriate  
✅ Monitor application health (Actuator)

---

**Happy Learning! 🚀**
