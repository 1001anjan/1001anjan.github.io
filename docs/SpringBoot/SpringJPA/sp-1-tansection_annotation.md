---
layout: default
title: @Transactional
parent: Spring JPA
grand_parent: Spring Boot
nav_order: 1
---
# @Transactional Annotation in Spring Boot
The @Transactional annotation is a cornerstone of transaction management in Spring Boot applications. It ensures data consistency by guaranteeing that a series of database operations are treated as a single unit of work. Within a transaction, either all operations succeed, or all are rolled back in case of an exception.

## Key Points:
* Automatic Rollback on Runtime Exceptions: By default, Spring rolls back transactions when runtime exceptions (e.g., RuntimeException, unchecked exceptions) occur within a transaction. Checked exceptions (e.g., IOException) do not trigger automatic rollback.
* Customizing Rollback Behavior: You can fine-tune transaction behavior using the rollbackFor and noRollbackFor attributes within @Transactional.
* Transactional Methods: Mark methods with @Transactional to indicate they participate in a transaction.
* Transactional Classes: Apply @Transactional at the class level to make all public methods within the class transactional by default.
* Transaction Scopes: Transactions can span across multiple methods and classes if they are nested within each other (inner methods inherit the transaction from outer methods).

## Complete Spring Boot Example:
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;
import org.springframework.transaction.annotation.Transactional;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
class Product {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;

    // Getters and setters
    // Constructor
}

@Repository
interface ProductRepository extends JpaRepository<Product, Long> {
}

@Service
class ProductService {

    private final ProductRepository productRepository;

    ProductService(ProductRepository productRepository) {
        this.productRepository = productRepository;
    }

    @Transactional
    public Product createProduct(String name) {
        Product product = new Product();
        product.setName(name);
        return productRepository.save(product);
    }

    @Transactional(rollbackFor = Exception.class)
    public void updateProductName(Long id, String newName) throws Exception {
        Product product = productRepository.findById(id)
                .orElseThrow(() -> new Exception("Product not found with id: " + id));
        product.setName(newName);
        // Intentionally throwing exception to trigger rollback
        throw new RuntimeException("Simulating an error during update");
    }
}

@SpringBootApplication
public class SpringBootDemoApplication {
    
    public static void main(String[] args) {
        SpringApplication.run(SpringBootDemoApplication.class, args);
    }
}
```

To handle transactions across multiple methods in Spring Boot, you can use the `@Transactional` annotation at the service layer on methods that interact with the database. Here's how you can handle transactions across multiple methods:

```java
@Service
public class ProductService {

    private final ProductRepository productRepository;

    public ProductService(ProductRepository productRepository) {
        this.productRepository = productRepository;
    }

    @Transactional
    public void createProduct(String name) {
        Product product = new Product();
        product.setName(name);
        productRepository.save(product);
    }

    @Transactional
    public void updateProduct(Long productId, String newName) {
        Product product = productRepository.findById(productId)
                .orElseThrow(() -> new ProductNotFoundException("Product not found with id: " + productId));
        product.setName(newName);
        productRepository.save(product);
    }
    
    @Transactional
    public void deleteProduct(Long productId) {
        Product product = productRepository.findById(productId)
                .orElseThrow(() -> new ProductNotFoundException("Product not found with id: " + productId));
        productRepository.delete(product);
    }
}
```
In this example:
* Each method in the `ProductService` class is annotated with `@Transactional`. This ensures that each method is executed within a transactional context.
* When you call any of these methods, Spring Boot will start a transaction before the method is executed and commit the transaction after the method completes. If an exception occurs during the execution of any of these methods, Spring Boot will automatically roll back the transaction, ensuring data consistency.

Make sure that your Spring Boot application is properly configured to enable transaction management. You may need to include `@EnableTransactionManagement` in your main application class or configure a transaction manager bean.

## Class level @Transactional
The `@Transactional` annotation can be applied at both class and method levels in Spring. Here's a guideline for when to use class-level `@Transactional`:

* All Methods in the Class Need Transactional Support: If all public methods in a service class need transactional support with the same configuration, applying `@Transactional` at the class level can be convenient and DRY (Don't Repeat Yourself).
* Consistent Transaction Configuration: If all methods in the class require the same transactional behavior, such as propagation, isolation level, and rollback rules, applying `@Transactional` at the class level ensures consistent configuration across methods.
* Transactional Nature of the Entire Class: If the entire class logically represents a single unit of work that needs to be transactional, applying `@Transactional` at the class level makes the intention clear and simplifies the code.

However, there are some considerations and caveats to keep in mind:

* Overriding Method-Level Annotations: Method-level `@Transactional` annotations will override class-level annotations if both are present. This allows for flexibility in configuring specific methods differently if needed.
* Transaction Scope: Be aware that class-level transactional behavior applies to all public methods, including those inherited from parent classes or implemented through interfaces.
* Complexity and Maintenance: Applying transactional behavior at the class level can lead to more complexity and potentially obscure the transactional nature of individual methods. Ensure that it enhances code readability and maintainability rather than adding unnecessary complexity.

In summary, class-level `@Transactional` can be useful for providing a consistent transactional context across all methods in a service class, but it should be used judiciously and with consideration for the specific requirements and design of the application.

## @Transactional(isolation = Isolation.REPEATABLE_READ)
The `@Transactional` annotation in Spring Boot is used to define the scope of a transactional method. The isolation attribute specifies the isolation level for the transaction.

In the context of `@Transactional(isolation = Isolation.REPEATABLE_READ)`, the `Isolation.REPEATABLE_READ` isolation level ensures that the data read within the transaction remains consistent throughout the transaction's duration. This means that if a row is read multiple times within the same transaction, the values will remain consistent, even if other transactions are updating or deleting the data.

Here's a brief explanation of the `Isolation.REPEATABLE_READ` isolation level:

`REPEATABLE_READ`: In this isolation level, a transaction reads a snapshot of the database at the start of the transaction and holds locks on all data it reads or modifies until the transaction completes. This ensures that any data read during the transaction remains consistent, even if other transactions are updating or deleting the same data. However, new data inserted after the transaction starts may not be visible to the transaction until it commits.
In summary, using `@Transactional(isolation = Isolation.REPEATABLE_READ)` ensures that the data read within the transaction remains consistent, even if other transactions are modifying the data concurrently.

---
The `@Transactional(isolation = Isolation.REPEATABLE_READ)` annotation in Spring Boot specifies the isolation level for a transactional method. Isolation levels define how concurrent transactions see each other's changes in the database. In this case, Isolation.REPEATABLE_READ provides a specific level of isolation that guarantees certain properties within a transaction.

Here's a breakdown of the isolation level and its implications:

`Isolation.REPEATABLE_READ`:
Guarantees:
* Read Committed: A transaction can only read data that has been committed by other transactions before the current transaction started (prevents "dirty reads").
* Repeatable Read: If a transaction reads a row multiple times within its execution, it will always see the same version of the data, even if another transaction updates that row in between reads (prevents "non-repeatable reads").

However, it does not prevent phantom reads. This means a transaction might not see rows that were inserted by other transactions after the current transaction started its initial read.

Use Cases for `Isolation.REPEATABLE_REA`D:

* Scenarios where you need to ensure consistency when reading data multiple times within a transaction.
* Situations where you need to avoid "dirty reads" and "non-repeatable reads" but can tolerate "phantom reads" (e.g., reports or summaries that might miss newly inserted data).

Comparison with Other Isolation Levels:

* READ_UNCOMMITTED: Lowest level, allows "dirty reads," "non-repeatable reads," and "phantom reads." Not recommended for most use cases.
* READ_COMMITTED: Prevents "dirty reads" but allows "non-repeatable reads" and "phantom reads." More commonly used than `READ_UNCOMMITTED` but might not be suitable for all scenarios.
* SERIALIZABLE: Strictest level, ensures serializability (transactions are executed as if they were one after another). Can lead to performance overhead.
Things to Consider:

Choosing the appropriate isolation level is a balance between data consistency and performance.
`Isolation.REPEATABLE_READ` offers a good balance for scenarios where consistency for multiple reads within a transaction is important, but "phantom reads" are acceptable.
If you need to completely prevent "phantom reads," consider using `@Transactional(isolation = Isolation.SERIALIZABLE)`, but be aware of potential performance implications.
Additional Tips:

If performance is a major concern, you can experiment with lower isolation levels like `READ_COMMITTED`, but only if you understand the potential data consistency issues.
Thoroughly test your transactions with different isolation levels to ensure they behave as expected and maintain data integrity in your application.

---
In most cases, you don't necessarily need to use the `@Transactional` annotation directly on repository methods (like saveOrder or savePayment in your example) when using Spring Data JPA. Here's why:

Spring Data JPA and Transaction Management: Spring Data JPA already provides built-in transaction management for CRUD operations (Create, Read, Update, Delete) on entities. When you call methods like save, findById, deleteById, etc., Spring Data JPA automatically manages the transaction for you.
`@Modifying` Annotation (Optional): If your repository method performs a custom query that modifies data (e.g., a bulk update query), you might need to use the `@Modifying` annotation alongside the query. This tells Spring Data JPA to treat the query as an update operation and handle the transaction accordingly.

Here's a breakdown of different scenarios:

## CRUD Operations:

For standard CRUD operations, you don't need `@Transactional` on the repository method. Spring Data JPA handles the transaction automatically.

```Java
public interface OrderRepository extends CrudRepository<Order, Long> {
Order findById(Long id); // No @Transactional needed, handled by Spring Data JPA
void deleteById(Long id); // No @Transactional needed, handled by Spring Data JPA
}
```



