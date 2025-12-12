

# # **🔥 Complete Spring Boot Notes + Interview Questions (MD Format)**

---

# # **📌 1. Introduction to Spring Boot**

Spring Boot is a framework built on top of Spring that helps developers build production-grade applications quickly with minimal configuration.

### **⭐ Key Features**

* Auto-configuration
* Embedded servers (Tomcat/Jetty/Netty)
* Production-ready (Actuator, Metrics)
* Simplified Dependency Management (Spring Starter Dependencies)
* Easy to create REST APIs
* Supports Microservices Architecture

---

# # **📌 2. Layer-Based Architecture in Spring Boot**

Spring Boot projects commonly follow **4-layered architecture**:

```
controller  
service  
repository  
model/entity  
config  
```

### **🔹 Layer Description**

| Layer              | Purpose                                |
| ------------------ | -------------------------------------- |
| **Controller**     | Handles HTTP requests (REST endpoints) |
| **Service**        | Business logic                         |
| **Repository**     | DB operations using JPA/Hibernate      |
| **Entity / Model** | Maps DB table                          |
| **Config**         | Java-based configurations              |

---

# # **📌 3. Development Order (BEST PRACTICE)**

1. **Entity (Model)**
2. **Repository**
3. **Service** (Optional but recommended)
4. **Controller**
5. **DTO (if needed)**

---

# # **📌 4. Creating Spring Boot Project**

Use **Spring Initializr**:
👉 [https://start.spring.io/](https://start.spring.io/)

### **Recommended Setup**

* **Project:** Maven
* **Language:** Java
* **Spring Boot Version:** Latest stable
* **Packaging:** Jar
* **Java Version:** 17 or 21

### **Dependencies to Add**

* Spring Web
* Spring Data JPA
* MySQL Driver
* Lombok
* (Optional) Spring Boot DevTools
* (Optional) Thymeleaf (for UI)

---

# # **📌 5. Maven vs Gradle**

| Topic        | Maven         | Gradle                      |
| ------------ | ------------- | --------------------------- |
| Build Type   | XML (pom.xml) | Groovy/Kotlin DSL           |
| Speed        | Slower        | Faster (incremental builds) |
| Flexibility  | Less flexible | Highly flexible             |
| Plugins      | More          | Less                        |
| Industry Use | Very common   | Increasing rapidly          |

---

# # **📌 6. Why Use `com.example` in Packages?**

Industry standard:
Companies reverse their domain:

example.com → `com.example.projectname`

This avoids naming conflicts.

---

# # **📌 7. Configuration (`application.properties`)**

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/database_name?createDatabaseIfNotExist=true
spring.datasource.username=root
spring.datasource.password=your_password

spring.jpa.show-sql=true
spring.jpa.hibernate.ddl-auto=update
spring.jpa.properties.hibernate.format_sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect

server.port=9999
```

### **Important**

* Change `database_name`
* Provide your MySQL username and password
* `ddl-auto=update` auto creates/updates tables

---

# # **📌 8. CRUD Flow in Spring Boot**

✔ CREATE → POST
✔ READ → GET
✔ UPDATE → PUT
✔ DELETE → DELETE

---

# # **📌 9. Files and Folder Structure**

```
src
 └── main/java/com/project
       ├── controller
       ├── service
       ├── repository
       ├── entity
       └── config
```

---

# # **📌 10. Product Management CRUD Code (Complete Example)**

### **Entity**

```java
@Entity
@Table(name = "product")
@Getter @Setter
@NoArgsConstructor @AllArgsConstructor
public class Product {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int id;

    private String name;
    private String description;
    private double price;
}
```

---

### **Repository**

```java
@Repository
public interface ProductRepository extends JpaRepository<Product, Integer> {}
```

---

### **Service**

```java
@Service
public class ProductService {

    @Autowired
    private ProductRepository productRepository;

    public Product addProduct(Product product) {
        return productRepository.save(product);
    }

    public List<Product> getAllProduct() {
        return productRepository.findAll();
    }

    public Product updateProduct(Product product) {
        Product existingProduct =
                productRepository.findById(product.getId()).orElse(null);

        if (existingProduct == null) {
            return null;
        }

        existingProduct.setName(product.getName());
        existingProduct.setDescription(product.getDescription());
        existingProduct.setPrice(product.getPrice());

        return productRepository.save(existingProduct);
    }

    public String deleteById(int id) {
        Product existingProduct =
                productRepository.findById(id).orElse(null);

        if (existingProduct == null) {
            return "Product not found";
        }

        productRepository.deleteById(id);
        return "Deleted product id: " + id;
    }
}
```

---

### **Controller**

```java
@RestController
@RequestMapping("/product")
public class ProductController {

    @Autowired
    private ProductService productService;

    @PostMapping
    public Product addProduct(@RequestBody Product product) {
        return productService.addProduct(product);
    }

    @GetMapping
    public List<Product> getAllProduct() {
        return productService.getAllProduct();
    }

    @PutMapping
    public Product updateProduct(@RequestBody Product product) {
        return productService.updateProduct(product);
    }

    @DeleteMapping("/{id}")
    public String deleteProduct(@PathVariable int id) {
        return productService.deleteById(id);
    }
}
```

---

# # **📌 11. @Autowired vs @RequiredArgsConstructor**

| Feature               | @Autowired | @RequiredArgsConstructor |
| --------------------- | ---------- | ------------------------ |
| Supported in          | Spring     | Lombok                   |
| Constructor injection | Manual     | Auto generated           |
| Best practice         | ❌ old      | ✅ modern                 |
| Clean code            | Less       | More                     |

---

# # **📌 12. Important Annotations in Spring Boot**

| Annotation        | Purpose                              |
| ----------------- | ------------------------------------ |
| `@RestController` | Combines @Controller + @ResponseBody |
| `@RequestMapping` | Base URL                             |
| `@GetMapping`     | Read                                 |
| `@PostMapping`    | Create                               |
| `@PutMapping`     | Update                               |
| `@DeleteMapping`  | Delete                               |
| `@Entity`         | DB table mapping                     |
| `@Id`             | Primary key                          |
| `@GeneratedValue` | Auto increment                       |
| `@Service`        | Business layer                       |
| `@Repository`     | Data layer                           |
| `@Autowired`      | Dependency injection                 |
| `@Table`          | Table name                           |

---

# # **📌 13. Spring Boot Life Cycle**

1. Load Config
2. Auto-Configuration
3. Create Beans
4. Run Application
5. Handle Requests
6. Shutdown gracefully

---

# # **📌 14. Spring Boot Important Interview Questions (With Answers)**

---

## **1. What is Spring Boot?**

Spring Boot is a framework built on top of Spring that simplifies application development with auto-configuration and embedded servers.

---

## **2. What is the difference between Spring and Spring Boot?**

| Spring               | Spring Boot        |
| -------------------- | ------------------ |
| Manual configuration | Auto-configuration |
| No embedded server   | Embedded server    |
| More boilerplate     | Less code          |
| Complex XML          | No XML             |

---

## **3. What is Dependency Injection?**

Process of providing dependencies (objects) to a class instead of creating them inside the class.

---

## **4. @Component, @Service, @Repository differences?**

| Annotation  | Layer          |
| ----------- | -------------- |
| @Component  | Generic bean   |
| @Service    | Business logic |
| @Repository | DB access      |

---

## **5. What is @RestController?**

Controller that returns JSON instead of HTML.

---

## **6. What is JPA?**

Java Persistence API → ORM standard.

---

## **7. What is Hibernate?**

Hibernate is an ORM implementation that JPA uses.

---

## **8. What is the purpose of application.properties?**

To configure:

* DB connection
* Port number
* Hibernate settings
* Custom configs

---

## **9. What is @RequestBody?**

Reads JSON from request and converts (deserializes) to Java object.

---

## **10. What is @PathVariable?**

Extracts value from URL.

---

## **11. What is the difference between PUT and PATCH?**

| PUT                    | PATCH                   |
| ---------------------- | ----------------------- |
| Full update            | Partial update          |
| Replaces entire object | Updates selected fields |

---

## **12. What is the use of `@Autowired`?**

Used for Dependency Injection (DI).

---

## **13. What is the Spring Boot Starter?**

Pre-configured dependencies.
Example: `spring-boot-starter-web`

---

## **14. What is `spring-boot-devtools`?**

Auto-reloading during development.

---

## **15. What is the purpose of `@Entity`?**

Marks a class as a table in the database.

---

## **16. How does Spring Boot connect to MySQL?**

Using JDBC URL inside `application.properties`.

---

## **17. What is Actuator in Spring Boot?**

Used for monitoring and exposing application health/metrics.

---

## **18. What is Autoconfiguration?**

Spring Boot auto-configures beans based on jar dependencies.

---

## **19. Explain Bean life cycle.**

Initialization → Use → Destroy

---

## **20. What is the difference between @Controller and @RestController?**

| @Controller        | @RestController   |
| ------------------ | ----------------- |
| Returns HTML pages | Returns JSON      |
| Used in web MVC    | Used in REST APIs |

---

# # ✅ Want MORE?
