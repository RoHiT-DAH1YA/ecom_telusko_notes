## get one product by id

ProductController
```java
@GetMapping("/product/{id}")  
public Product getProduct(@PathVariable int id){  
    return service.getProductById(id);  
}
```
ProductService
```java
public Product getProductById(int id) {  
    return repo.findById(id).orElse(new Product());  
}
```

## handling date format using jackson library
model  > Product.java
```java
@JsonFormat(shape = JsonFormat.Shape.STRING, pattern = "dd-mm-yyyy")  
private Date releaseDate;
```

## returning a ResponseEntity
- benefit of using response entity is that we can configure things like http status
	```java 
```