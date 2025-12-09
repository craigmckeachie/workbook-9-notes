
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

## 🟧 **Dependencies**

* **Maven Dependency** — “Give me this toolbox (a library).”
* **Spring Dependency (Injection)** — “Give me this particular tool from the toolbox.”

---

If you want this as a **PDF**, **slide**, or **print-friendly layout**, I can generate that too.
