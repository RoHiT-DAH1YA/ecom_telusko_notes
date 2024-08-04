## How to resolve it
- add @CrossOrigin on the controller classes
-  not CorsOrigin

```java
@RestController  
@CrossOrigin
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

