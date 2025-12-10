1. Difference between Spring Bean and Java Bean?

   - **Spring Bean** — an object Spring manages.
   - **Java Bean** — a simple model object, Plain old Java Object (POJOs) (fields + getters/setters).

2. What objects are managed by Spring? Why are the models objects not managed by Spring?
   - Spring doesn't manage model objects because they're simple data structures, whereas other objects like DAOs and controllers require Spring's features for their functionality and interaction.

3. What are the Annotations that create objects? 
   - Stereotype Annotations tell Spring _WHAT_ to create

   - **@Component** — Spring, create an object/instance of this class (Spring calls that instance a Spring Bean).

    ```Java
    @Component
    public class ProductDao{

    }

    //  You write this part:
    ProductDao productDao;

    //Spring does this for you.
    ProductDao productDao = new ProductDao();
    ```

    If Spring is going to new up an object for you. It needs a default (parameterless) constructor.

4. How are these Stereotype Annotations different?
   - @Component vs @Service vs @Repository
   - short answer: they aren't, Spring does the same thing for all of them
   - @Component describes a class as being a baseball player
   - @Service and @Repository describes a class more specifically
     - @Service - I am a third-baseman
     - @Repository- I am the left fielder 
     - **@Service** — This is business logic; treat it like a component.
     - **@Repository** — This talks to the DB; treat it like a component.

5. @Autowired (Inject) — “Give me the object you created for me.”
   - For example the UserInterface class might need an instance of the ProductDao to get data
   ```Java
   public class UserInterface{
     //without Spring we would do this
      ProductDao productDao = new ProductDao();

      //with Spring we would do this
      @Autowired
      ProductDao productDao;

        public void displayAllProducts(){

            List<Product> products = productDao.getAll();
            System.out.println(products);
        }

   }
   ```




-----

## 🛠️ Autowiring Methods with `@Autowired`

Q: What are the different ways to Autowire or Inject an object.

Here are the three primary methods for dependency injection in Spring, demonstrated with the `UserInterface` and `ProductDao` example.

### 1\. Field Injection (Simplest, but not Best Practice)

The `@Autowired` annotation is placed directly on the field. Spring uses reflection to inject the dependency.

#### Example Implementation

```java
import java.util.List;

// @Component (or @Service, @Controller) indicates Spring manages this class
public class UserInterface {

    // Inject the dependency directly onto the field
    @Autowired
    private ProductDao productDao;

    public void displayAllProducts() {
        System.out.println("--- Using Field Injection (Least Recommended) ---");
        List<Product> products = productDao.getAll();
        System.out.println(products);
    }
}
```

### 2\. Constructor Injection (Recommended Practice)

The dependency is provided as an argument to the class's constructor. This ensures the class is fully initialized with all dependencies upon creation.

#### Example Implementation

```java
import java.util.List;

// @Component (or @Service, @Controller) indicates Spring manages this class
public class UserInterface {

    // 1. Declare the dependency as a final private field.
    private final ProductDao productDao;

    // 2. Explicitly place @Autowired on the constructor.
    //    (Spring uses this constructor to create the bean.)
    @Autowired
    public UserInterface(ProductDao productDao) {
        // 3. Assign the injected dependency to the final field.
        this.productDao = productDao;
    }

    public void displayAllProducts() {
        System.out.println("--- Using Constructor Injection (Recommended) ---");
        List<Product> products = productDao.getAll();
        System.out.println(products);
    }
}
```

  * **Key Advantage:** It allows the dependency to be `final`, promoting **immutability** and **thread safety**. It also makes the class straightforward to **unit test** without needing the Spring container.

### 3\. Setter Injection (Best for Optional Dependencies)

The dependency is provided via a standard setter method. Spring calls this method after the object has been instantiated.

#### Example Implementation

```java
import java.util.List;

// @Component (or @Service, @Controller) indicates Spring manages this class
public class UserInterface {

    // 1. Declare the dependency (must not be final).
    private ProductDao productDao;

    // 2. Place @Autowired on the setter method.
    //    (Spring calls this method to set the dependency.)
    @Autowired
    public void setProductDao(ProductDao productDao) {
        // 3. Assign the injected dependency to the field.
        this.productDao = productDao;
    }

    public void displayAllProducts() {
        System.out.println("--- Using Setter Injection ---");
        List<Product> products = productDao.getAll();
        System.out.println(products);
    }
}
```

  * **Key Advantage:** It allows you to **change** the dependency after the object is created, and it's useful for **optional** dependencies that aren't strictly required for the class to function.

-----

