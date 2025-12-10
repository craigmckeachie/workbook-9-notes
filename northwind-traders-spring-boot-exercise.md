# 🛒 NorthwindTradersSpringBoot - Product Management CLI

This exercise guides you through building a simple admin interface for managing products using Spring Boot, JDBC, and the Northwind database.

---

## ✅ Exercise 1: Create a New Spring Boot Project

You will create a new Java Maven project using **Spring Boot**.

1. Open a browser and go to the following link:  
   👉 [Generate Spring Boot Project](https://start.spring.io/#!type=maven-project&language=java&platformVersion=3.5.0&packaging=jar&jvmVersion=17&groupId=com.pluralsight&artifactId=NorthwindTradersSpringBoot&name=NorthwindTradersSpringBoot&description=Demo%20project%20for%20Spring%20Boot&packageName=com.pluralsight.NorthwindTradersSpringBoot&dependencies=web)

2. The project will already be configured with:

   - **Project Type:** Maven Project
   - **Language:** Java
   - **Spring Boot Version:** 4.0.0
   - **Group:** `com.pluralsight`
   - **Artifact:** `NorthwindTradersSpringBoot`
   - **Name:** `NorthwindTradersSpringBoot`
   - **Description:** Demo project for Spring Boot
   - **Package name:** `com.northwind.trading`
   - **Packaging:** Jar
   - **Java Version:** 17
   - **Dependencies:** Spring Web

3. Click **Generate** to download the project zip file.

4. Unzip the downloaded file to your `workbook-9` folder.

5. Open the project in IntelliJ and run the application to verify it starts successfully.

---

## ✅ Exercise 2: Create a Product Model, DAO, and CLI Interface

### 🧱 Step 1: Add the code to see what beans are being created by Spring to `NorthwindTradersSpringBootApplication` using the Sakila example below

```Java
package com.pluralsight.SakilaSpringBoot;


import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;

@SpringBootApplication
public class SakilaSpringBootApplication {

    public static void main(String[] args) {

        // This line starts the entire Spring Boot application.
        // It does 3 main things:
        // 1. Creates the Spring "ApplicationContext" (this is like the brain of Spring that manages everything).
        // 2. Scans for your @Component classes and creates them automatically.
        // 3. Starts the web server (if your app had web controllers), or calls CommandLineRunner beans.
        ApplicationContext context = SpringApplication.run(SakilaSpringBootApplication.class, args);


        // After the line above runs, your app is running!
        // If you have a CommandLineRunner (like UserInterface), its run() method will now be called.
        //It does this for you.
        // UserInterface userInterface = new UserInterface();
        // userInterface.run()

        //This is just logging code to show you what Spring Boot is doing.
        //More specifically, it's showing you which objects it created for you.
        String[] beanNames = context.getBeanDefinitionNames();

        System.out.println("\nMy Application Beans:");
        for (String beanName : beanNames) {
            Object bean = context.getBean(beanName);
            String packageName = bean.getClass().getPackageName();

            if (packageName.startsWith("com.pluralsight.SakilaSpringBoot")) {
                System.out.println(beanName + " -> " + bean.getClass().getSimpleName());
            }
        }
    }

}

```

### 🧱 Step 1: Create the Product model

Inside the `com.northwind.trading.model` package, create a `Product` class with the following fields:

```java
private int productId;
private String name;
private int categoryId;
private double price;
```

Generate getters, setters, and a constructor.

---

### 🧩 Step 2: Create a DAO Interface

In the `com.northwind.trading.data` package, create an interface named `ProductDao` with the following method signatures:

```java
Product add(Product product);
List<Product> getAll();
```

You may optionally add methods later for delete, update, or search.

---

### 💾 Step 3: Create the ProductDaoInMemory

Create a class named `ProductDaoInMemory` that implements the `ProductDao` interface. It should:

- Use `@Component` to register as a Spring bean
- Implement the `add()` and `getAll()` methods as we did in [Sakila with Actor](https://github.com/craigmckeachie/SakilaSpringBoot/blob/main/src/main/java/com/pluralsight/sakila/data/ActorDaoInMemory.java)

---

## 🏃 Step 4: Build the CLI Application

Create a new class called `UserInterface` in the `com.northwind.trading.ui` package. This class must:

- Implement `CommandLineRunner`
- Autowire the `ProductDao` interface using:

```java
@Autowired
private ProductDao productDao;
```

- Contain your UI logic in the `run()` method:
  - List products
  - Add a new product

---

## 🛠 Step 5: Configure Your Database Connection

Open `src/main/resources/application.properties` and add the following values (with your real credentials):

```properties
datasource.url=jdbc:mysql://localhost:3306/northwind
datasource.username=yourUsername
datasource.password=yourPassword
```

Create a class named `DatabaseConfiguration` in the `config` package. It should:

- Use `@Configuration`
- Have a `@Bean` method that returns a `DataSource` using `BasicDataSource`
- Read properties using `@Value`
- Add these line to the constructor so you can verify that the values are being read from the properties file.

```Java
 System.out.println(url);
 System.out.println(username);
 System.out.println(password);
```

You’ll need to add the following dependencies to your `pom.xml`:

```xml
<dependency>
   <groupId>mysql</groupId>
   <artifactId>mysql-connector-java</artifactId>
   <version>8.0.33</version>
</dependency>
<dependency>
   <groupId>org.apache.commons</groupId>
   <artifactId>commons-dbcp2</artifactId>
   <version>2.13.0</version>
</dependency>
```


