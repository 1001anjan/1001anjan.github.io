---
layout: default
title: Entity Mapping Example
parent: Spring JPA
grand_parent: Spring Boot
nav_order: 1
---
# Entity Mapping Example
```java
@Entity
public class Employee {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private BigDecimal salary;

    @ManyToOne
    @JoinColumn(name = "department_id")
    private Department department;

    @OneToMany(mappedBy = "employee", cascade = CascadeType.ALL)
    private List<Address> addresses = new ArrayList<>();

    // Getters and setters
}

@Entity
public class Department {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    // Getters and setters
}

@Entity
public class Address {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String city;
    private String street;

    @ManyToOne
    @JoinColumn(name = "employee_id")
    private Employee employee;

    // Getters and setters
}

```
```java
@Repository
public interface EmployeeRepository extends JpaRepository<Employee, Long> {

    List<Employee> findByDepartmentId(Long departmentId);

    List<Employee> findByAddressesCity(String city);

    @Query("SELECT e FROM Employee e WHERE e.department.id = :departmentId " +
           "AND e.salary = (SELECT MAX(e2.salary) FROM Employee e2 WHERE e2.department.id = :departmentId)")
    List<Employee> findEmployeesWithMaxSalaryByDepartment(@Param("departmentId") Long departmentId);
}

@Repository
public interface DepartmentRepository extends JpaRepository<Department, Long> {
}

@Repository
public interface AddressRepository extends JpaRepository<Address, Long> {
}
```
```java
@RestController
@RequestMapping("/employees")
public class EmployeeController {

    @Autowired
    private EmployeeService employeeService;

    @GetMapping("/by-department/{departmentId}")
    public List<Employee> getEmployeesByDepartment(@PathVariable Long departmentId) {
        return employeeService.getEmployeesByDepartment(departmentId);
    }

    @GetMapping("/by-address/{city}")
    public List<Employee> getEmployeesByAddress(@PathVariable String city) {
        return employeeService.getEmployeesByAddress(city);
    }

    @GetMapping("/max-salary-by-department/{departmentId}")
    public List<Employee> getEmployeesWithMaxSalaryByDepartment(@PathVariable Long departmentId) {
        return employeeService.getEmployeesWithMaxSalaryByDepartment(departmentId);
    }
}

@RestController
@RequestMapping("/departments")
public class DepartmentController {

    @Autowired
    private DepartmentService departmentService;

    @GetMapping
    public List<Department> getAllDepartments() {
        return departmentService.getAllDepartments();
    }
}

@RestController
@RequestMapping("/addresses")
public class AddressController {

    @Autowired
    private AddressService addressService;

    @GetMapping
    public List<Address> getAllAddresses() {
        return addressService.getAllAddresses();
    }
}
```

### `@ManyToOne`:
* This annotation is used to define a many-to-one relationship between two entities in a JPA (Java Persistence API) application.
In the context of example, it is used in the `Employee` entity to represent the relationship between an employee and their department. It means that many employees can belong to one department.

### `@JoinColumn`:
* This annotation specifies the name of the column that is used for joining an entity association or element collection.
In the example, it specifies the name of the column in the Employee table that is used to store the foreign key referencing the id column of the Department table. This column is named `department_id`.

### `@OneToMany`:
* This annotation is used to define a one-to-many relationship between two entities in a JPA application.
* In the context of example, it is used in the Department entity to represent the relationship between a department and its employees. It means that one department can have many employees.

### `mappedBy` attribute:
* This attribute is used to specify the property of the target entity that owns the relationship. It is used in a bidirectional one-to-many or many-to-one relationship.
* In the example, it is used in the @OneToMany annotation in the Department entity to specify that the employee field in the Employee entity is the owning side of the relationship. This means that the Employee entity is responsible for managing the relationship.

### `cascade` attribute:
* This attribute specifies which operations should be cascaded from the parent entity to the associated entities.
* In your example, `CascadeType.ALL` is used to specify that all operations (including persist, merge, remove, refresh) should be cascaded from the Employee entity to its associated Address entities. This means that when an Employee entity is persisted, merged, removed, or refreshed, the corresponding operations will also be applied to its associated Address entities.