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
    class ProductDao{

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

5. @Autowired

6. @Bean how is it different than @Component?
7. How does @Configuration work, what does it do?
8. How to control name of object created for you?
9. Explain page 53, 54
