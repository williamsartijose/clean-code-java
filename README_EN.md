# clean-code-java

## Table of Contents
1. [Introduction](#introduction)
2. [Variables](#variables)
3. [Methods](#methods)
4. [Objects and Data Structures](#objects-and-data-structures)
5. [Classes](#classes)
6. [SOLID](#solid)
7. [Testing](#testing)
8. [Concurrency](#concurrency)
9. [Error Handling](#error-handling)
10. [Formatting](#formatting)
11. [Comments](#comments)
12. [Translations](#translations)

## Introduction
![Imagem humorística da estimativa de qualidade do software baseado na contagem de quantos palavrões você gritou enquanto lia o código.](http://www.osnews.com/images/comics/wtfm.jpg)


Software Engineering Principles, from Robert C. Martin's book Clean Code, adapted for JavaScript. This is not a style guide. It is a guide to producing readable, reusable, and refactorable code in JavaScript.

Not every principle demonstrated should be followed strictly, and even fewer are universally agreed upon. These principles are guidelines and nothing more, yet they have been codified through many years of collective experience by the authors of Clean Code.

Our craft of software engineering is just over 50 years old, and we are still learning a lot. When software architecture is as old as building architecture, perhaps then we will have stricter rules to follow. For now, let these guidelines serve as a criterion for evaluating the quality of the JavaScript code you and your team produce.

One more thing: learning this won't instantly make you a better software developer, and working with these principles for many years doesn’t mean you won’t make mistakes. Every piece of code starts as a draft, like wet clay being shaped into its final form. Ultimately, we carve out imperfections when we review with our peers. Don’t feel guilty about early drafts that still need improvement. Instead, take it out on your code.


## **Variables**

### Use descriptive and pronounceable variable names

**Bad:**
```java
String a = "2024-09-15";
```

**Good:**
```java
String currentDate = "2024-09-15";
```

### Use camelCase for variable and method names

**Bad:**
```java
String Current_Date = "2024-09-15";
```

**Good:**
```java
String currentDate = "2024-09-15";
```

### Avoid unnecessarily complex variable names

**Bad:**
```java
int wxyz = calculate();
```

**Good:**
```java
int totalCost = calculate();
```

### Use constants for "magic numbers"

**Bad:**
```java
if (user.age > 18) {
    // code
}
```

**Good:**
```java
private static final int ADULT_AGE = 18;

if (user.age > ADULT_AGE) {
    // code
}
```

## **Methods**

### Keep methods short and focused on a single task

**Bad:**
```java
public void saveUser(User user) {
    validateUser(user);
    logUserSaveAttempt(user);
    database.save(user);
    emailService.sendConfirmation(user);
}
```

**Good:**
```java
public void saveUser(User user) {
    validateUser(user);
    logUserSaveAttempt(user);
    saveToDatabase(user);
    sendConfirmationEmail(user);
}

private void saveToDatabase(User user) {
    database.save(user);
}

private void sendConfirmationEmail(User user) {
    emailService.sendConfirmation(user);
}
```

### Use descriptive method names

**Bad:**
```java
public void handle() {
    // code
}
```

**Good:**
```java
public void processUserRegistration() {
    // code
}
```

### Avoid methods with too many parameters

**Bad:**
```java
public void createUser(String name, String email, int age, String address, String phone) {
    // code
}
```

**Good:**
```java
public void createUser(UserDTO userDTO) {
    // code
}
```

## **Objects and Data Structures**

### Avoid exposing internal details of objects

**Bad:**
```java
public class User {
    public String name;
    public String email;
}
```

**Good:**
```java
public class User {
    private String name;
    private String email;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}
```

## **Classes**

### Apply the Single Responsibility Principle

Each class should have a single responsibility or purpose. Break down large, complex classes into smaller, more manageable ones.

**Bad:**
```java
public class UserService {
    public void createUser() { /* creation logic */ }
    public void sendWelcomeEmail() { /* email logic */ }
    public void validateUser() { /* validation logic */ }
}
```

**Good:**
```java
public class UserService {
    public void createUser() { /* creation logic */ }
}

public class EmailService {
    public void sendWelcomeEmail() { /* email logic */ }
}

public class UserValidator {
    public void validateUser() { /* validation logic */ }
}
```

## **SOLID**
Apply the SOLID principles:
- **S**: Single Responsibility Principle
- **O**: Open/Closed Principle
- **L**: Liskov Substitution Principle
- **I**: Interface Segregation Principle
- **D**: Dependency Inversion Principle

**Example of applying the OCP (Open/Closed Principle):**

**Bad:**
```java
public class Invoice {
    public double calculateTotal() {
        // calculation logic
    }
}
```

**Good:**
```java
public interface Invoice {
    double calculateTotal();
}

public class RegularInvoice implements Invoice {
    @Override
    public double calculateTotal() {
        // calculation logic
    }
}

public class DiscountedInvoice implements Invoice {
    @Override
    public double calculateTotal() {
        // calculation logic with discount
    }
}
```

## **Error Handling**

### Don't ignore exceptions

**Bad:**
```java
try {
    // code
} catch (Exception e) {
    // do nothing
}
```

**Good:**
```java
try {
    // code
} catch (Exception e) {
    log.error("Error while executing operation", e);
}
```
---
## **Translations**

Translations are available in other languages:

- ![br](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Brazil.png) **Português**: [Boas práticas de código limpo em Java](https://github.com/seu-repositorio/README_BR)
- ![en](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/United-States.png) **English**: [Clean Code Best Practices in Java](https://github.com/seu-repositorio/README_EN)
- ![es](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Uruguay.png) **Español**: [Buenas prácticas de código limpio en Java](https://github.com/seu-repositorio/README_ES)



---
