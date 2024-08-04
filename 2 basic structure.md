There is always a 3 layer architecture
- Controller
- Service
- Repository

**Controller** -> layer is responsible to make the service layer accessible to the client side
**Service** -> layer is where all the business logic goes. It talks with repository layer if retrieval of some data set is required. It also talks with controller layer if some data is to be sent output is generated during its working.
**Repo** -> layer is responsible to deal with all type of data retrieval.

- this three layer architecture divides the complete server into manageable modules
- makes the testing of each part independent
- The Service layer can even be tested as a POJO, and by mocking Repository conditions we can test all the business logic therein without having to worry about going through the controller layer to test it.