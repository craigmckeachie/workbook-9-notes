
# 📝 **Spring & Spring Boot Cheat Sheet**


## **What Spring Does**

* **Spring creates objects for you** (called *Spring Beans*).
* **Spring = loose coupling** → easier to swap implementations.
* **Spring Bean** — an object Spring manages.
* **JavaBean** — a simple model object (fields + getters/setters).

---

## **Spring vs. Spring Boot**

* **Spring** — Powerful and flexible, but requires a lot of setup via configuration files.
* **Spring Boot** — Spring *already configured* for you.


---


## **IoC & DI**

* **IoC (Inversion of Control)** — “Don’t create objects yourself.”
* **DI (Dependency Injection)** — “Let Spring *give* you the objects.”
* **`@Autowired`** — “Give me the object you created for me.”

**When Spring has *multiple* possible beans to inject:**

* **`@Primary`** — “If there are several choices, this one wins by default.”
* **`@Qualifier("name")`** — “No, not that bean—give me *this specific one*.”




---

## **Annotations (What Spring pays attention to)**

**`@____`** = a tag telling Spring how to treat a class or method.

---

## 🟦 **Core Stereotype Annotations** (Tell Spring *WHAT* to create)

* **@Component** — Spring, create this class as a bean.
* **@Service** — This is business logic; treat it like a component.
* **@Repository** — This talks to the DB; treat it like a component.
* **@Controller** — Handles web requests (MVC).
* **@RestController** — Handles web requests and returns JSON.

---

## 🟩 **Configuration & Bean Management** (Tell Spring *HOW* to create things)

* **@Configuration** — This class defines beans.
* **@Bean** — The return value of this method is a Spring-managed object.
* **@Autowired** — Inject a bean here instead of using `new`.

---
## **Common Bean Injection Styles**

* **Constructor Injection (best)** — “Give me everything I need right when I’m created.”
* **Setter Injection** — “Give me objects through setter methods.”
* **Field Injection (not recommended)** — “Put it directly in my field.”

---

## 🟧 **Dependencies**

* **Maven Dependency** — “Give me this toolbox (a library).”
* **Spring Dependency (Injection)** — “Give me this particular tool from the toolbox.”




---

## **Scopes (How long Spring keeps a bean alive)**

* **Singleton (default)** — “Make ONE object for the whole app.”
* **Prototype** — “Make a NEW object every time I ask.”
* **Request** — “One object *per web request*.”
* **Session** — “One object *per user session*.”

---

## **Component Scanning**

* **Component Scan** — “Spring, look in this package and auto-find my classes.”
* By default, Spring Boot scans from your main class **downward**.

---



---

## **Spring Boot Auto-Configuration**

* “Spring Boot looks at what libraries you have and configures things automatically.”
* Example: If you include **Spring Web**, Boot creates a web server.
* Example: If you include **Spring Data JPA**, Boot configures Hibernate.

---

## **Properties & External Configuration**

* **application.properties / application.yml** — “My app’s settings go here.”
* Used to define things like database URLs, ports, and passwords.
* Spring can inject values using:
  `@Value("${property.name}")`

---

## **Profiles**

* **Profiles** — “Pick which configuration to use (dev, test, prod).”
* Example:
  `spring.profiles.active=dev`
* You can mark beans for certain environments with:
  `@Profile("dev")`

---

## **Spring Boot Starter Dependencies**

* **Starter** — “A bundle of libraries that work well together.”
* Examples:

  * `spring-boot-starter-web` — Web server, JSON, MVC
  * `spring-boot-starter-data-jpa` — Database + JPA
  * `spring-boot-starter-test` — Testing tools

---

