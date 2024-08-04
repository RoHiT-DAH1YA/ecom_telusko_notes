now we need to create basic structure
- controller
- service 
- repository
- model

# Now code for retrieving all products is written
For that we will require a
- product - Model
- product - Controller
- Product - Service 
- Product - repo
## create PRODUCT MODEL 
```java
@Entity  // for jpa to create a table by itself
@Data  // lombok - to create getters and setters
@AllArgsConstructor  // lombok - to create getters and setters
@NoArgsConstructor  // lombok - to create getters and setters
public class Product {  
  
	@Id  // for jpa to make id as pri key
	@GeneratedValue(strategy = GenerationType.IDENTITY) // helps to create ids on its own
    private int id;  
    private String name;  
    private String desc;  
    private String brand;  
    private BigDecimal price;  
    private String category;  
    private Date releaseDate;  
    private boolean available;  
    private int quantity;
}
```

## create Product Controller

```java
@RestController  
@RequestMapping("/api")  
public class ProductController {  
  
    @Autowired  
    private ProductService service;  
	// testing the website
    @RequestMapping("/")  
    public String greet() {  
        return "Hello World";  
    }  
	// requesting info of all products
    @GetMapping("/products")  
    public List<Product> getAllProducts() {  
        return service.getAllProducts();  
    }  
}
```

## next create Product Service

```java
@Service  
public class ProductService {  
    @Autowired  
    private ProductRepo repo;

	// requesting the repo to get all products info
    @GetMapping("/products")  
    public List<Product> getAllProducts() {  
        return repo.findAll();  
    }  
}
```

## create Product Repository
```java
// JapRepository <type_of_data_elements, type_od_pri_key>
public interface ProductRepo extends JpaRepository<Product, Integer> {}
```

- yes there is no implementation required of this interface
- `JpaRepository` interface will handle everything

### Result
- you will be able to get all the products from the database
- but the database is in memory so whenever you restart the program you need to again load the data
### Automate the loading of data
- create a file resources > data.sql
- in this file write the sql queries that needs to be executed to input sample data at the starting of the program.
```sql
insert into product(name,desc,brand,price,category, release_date, available, quantity) values  
('Tata Nexon', 'A compact SUV with exccellent safety features and performance', 'Tata Motors', 750000.0, 'Cars', '2024-01-15', true, 50),  
('Maruti Suzuki Swift', 'A compact SUV with exccellent safety features and performance', 'Maruti Suzuki', 550000.0, 'Cars', '2024-02-01', true, 100),  
('Hyundai Creta', 'A compact SUV with exccellent safety features and performance', 'Hyundai', 950000.0, 'Cars', '2024-03-01', true, 75),  
('Mahindra Thar', 'A compact SUV with exccellent safety features and performance', 'Mahindra', 1200000.0, 'Cars', '2024-04-01', true, 30),  
('Honda City', 'A compact SUV with exccellent safety features and performance', 'Honda', 1100000.0, 'Cars', '2024-05-01', true, 60);
```

- there will be an **error** while running the program. It occurs because spring try to execute the sql queries before the table is created by it. To solve that issue add following line to application.properties 
```java
spring.jpa.defer-datasource-initialization=true
```
