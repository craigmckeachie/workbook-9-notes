# Workbook 9 

- [SpringBootSakila](https://github.com/erics273/SpringBootSakila)
- [Northwind Exercise](https://gist.github.com/erics273/22c2890fc37c482c7e9dcf946053827b)



## Key Concepts

## Dependency

- Maven, pom.xml Dependency= library 
  - Spring the entire Framework is a library in a jar that can be installed this way
- Dependency Injection Framework (Spring) Dependency = object/instance of class

Here’s a **clean, clear table** summarizing the two meanings of “dependency” — one from **Maven** and one from **Spring Dependency Injection** — plus some augmentation to make the distinction unmistakable.

---

# ✅ **Dependency in Maven vs. Dependency in Spring (DI)**

| Concept                                    | “Dependency” Meaning              | What It Actually Is                        | Where It Comes From / Lives                         | How It’s Used                                                           | Example                                             |
| ------------------------------------------ | --------------------------------- | ------------------------------------------ | --------------------------------------------------- | ----------------------------------------------------------------------- | --------------------------------------------------- |
| **Maven Dependency**                       | A *library your project needs*    | A **JAR file** containing classes          | Defined in `pom.xml`, downloaded from Maven Central | Makes external code available to your project                           | `spring-core`, `mysql-connector-j`, `commons-dbcp2` |
| **Spring Dependency Injection Dependency** | An *object your class depends on* | An **instance of a class** (a Spring bean) | Created and managed by the Spring container         | Injected into other classes via constructor, setter, or field injection | Injecting `DataSource` into your repository         |

---

# 💡 How to Think About It

### ✔ Maven dependency → **code-level dependency**

* A library (JAR) your project needs to compile and run.
* Added in `pom.xml`.
* Example:

  ```xml
  <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
  </dependency>
  ```

### ✔ Spring DI dependency → **object-level dependency**

* A concrete Java object your class needs to do its work.
* Provided automatically by Spring.

Example:

```java
public class FilmRepository {
    private final DataSource dataSource;   // <-- dependency

    public FilmRepository(DataSource dataSource) {
        this.dataSource = dataSource;      // <-- injected by Spring
    }
}
```

---

# 🧠 Enriched Summary (Augmented)

| Layer         | What “Dependency” Means                                        | Analogy                                                |
| ------------- | -------------------------------------------------------------- | ------------------------------------------------------ |
| **Maven**     | “Give me this *toolbox*.”                                      | Bringing home a toolbox full of tools.                 |
| **Spring DI** | “Give me this *specific tool from the toolbox*, ready to use.” | Receiving a hammer that’s already assembled and tuned. |

---

If you'd like, I can also create a diagram showing the flow from:
**Maven JAR → Spring Bean → Injection into a class**



Here’s the difference in a clear, practical way:

---

# **Spring vs. Spring Boot (Straightforward Explanation)**

## **Spring Framework**

Spring is the *core* Java framework that provides:

* **Dependency Injection (IoC)**
* **AOP (Aspect-Oriented Programming)**
* **Spring MVC (web framework)**
* **Spring JDBC / Spring ORM**
* **Security**, **Transactions**, etc.

**But:**
Using plain Spring requires a *lot* of manual setup:

* Long XML configurations (or Java configs)
* You select and manage dependencies yourself
* You configure your own web server (Tomcat, Jetty, etc.)
* You write lots of boilerplate to get things running

**In short:**
Spring is powerful, flexible—but heavy to configure.

---

## **Spring Boot**

Spring Boot is **Spring with batteries included**.

It sits *on top* of Spring and does three big things:

### **1. Auto-configuration**

Boot inspects your project and automatically configures:

* Spring MVC
* DataSource
* JPA/Hibernate
* Security
* Message converters
  …based on the dependencies you include.

You no longer hand-wire everything.

---

### **2. Opinionated Defaults**

Boot gives you:

* sensible settings
* default directory structures
* production-ready defaults
  so you don’t start from zero.

---

### **3. Embedded Servers**

When you create a Boot app, you automatically get:

* **embedded Tomcat** (default)
* or Jetty / Undertow if you choose

This means:
**You run your app with:**

```
java -jar app.jar
```

No deployment to an external server.

---

## **Quick Analogy**

| Concept         | Analogy                                                                            |
| --------------- | ---------------------------------------------------------------------------------- |
| **Spring**      | A fully-stocked toolset—powerful, but requires you to assemble everything yourself |
| **Spring Boot** | A pre-assembled “starter kit” with auto-wiring, defaults, and a built-in engine    |

---

## **Which should you use?**

**Spring Boot** for modern development (99% of new projects).
**Spring** only if you need fine-grained control or maintain old legacy systems.

---

## **Shortest summary possible**

**Spring** = The framework
**Spring Boot** = Spring + auto-configuration + embedded server + faster development

---

If you'd like, I can also explain:

* How Boot “starter” dependencies work
* Why a POM in Boot pulls in so many Spring libraries
* The evolution from XML → Java Config → Boot

Here’s a clean, concise table that summarizes **IoC vs DI** exactly the way you described it:

---

## **IoC vs DI — Summary Table**

| Concept | Stands For           | What It Is             | Purpose                                                                                | Who Controls Object Creation?                | Relationship                          |
| ------- | -------------------- | ---------------------- | -------------------------------------------------------------------------------------- | -------------------------------------------- | ------------------------------------- |
| **IoC** | Inversion of Control | A **principle / idea** | Shift control of object creation/lifecycle away from your code                         | **Framework/container**                      | DI is one way to implement IoC        |
| **DI**  | Dependency Injection | A **design pattern**   | Provide an object's dependencies from the outside rather than creating them internally | **Framework/container injects dependencies** | DI is a technique used to achieve IoC |

---

### **One-sentence version**

* **IoC** = high-level concept (“don’t control object creation yourself”)
* **DI** = concrete pattern (“inject the objects instead of creating them”)

---

If you want, I can also show a simple Java example of IoC vs DI in code.


