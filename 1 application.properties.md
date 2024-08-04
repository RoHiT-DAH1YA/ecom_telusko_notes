- `application.properties` is a file to configure the project (not spring)
```java
spring.application.name=ecom-proj

//link for jdbc connection
spring.datasource.url-jdbc:h2:mem:rohit
// name of database driver used
spring.datasource.driverClassName=org.h2.Driver

// show all sql querries that ran in terminal
spring.jpa.show-sql=true
/* when we want jpa to create the table
we encounter a problem that every time the programs starts
we need to update the table for databases 
like mysql or postgres
its not neede for in memory datanases like h2 but still its 
good to have it
*/
spring.jpa.hibernate.ddl-auto=update
```