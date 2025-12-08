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
