# clean-code-java

## Índice
1. [Introducción](#introducción)
2. [Variables](#variables)
3. [Métodos](#métodos)
4. [Objetos y Estructuras de Datos](#objetos-y-estructuras-de-datos)
5. [Clases](#clases)
6. [SOLID](#solid)
7. [Pruebas](#pruebas)
8. [Concurrencia](#concurrencia)
9. [Manejo de Excepciones](#manejo-de-excepciones)
10. [Formateo](#formateo)
11. [Comentarios](#comentarios)
12. [Traducciones](#traducciones)

## Introducción
![Imagem humorística da estimativa de qualidade do software baseado na contagem de quantos palavrões você gritou enquanto lia o código.](http://www.osnews.com/images/comics/wtfm.jpg)

Principios de Ingeniería de Software, del libro Clean Code de Robert C. Martin, adaptados para JavaScript. Esto no es una guía de estilos. Es una guía para producir código legible, reutilizable y refactorizable en JavaScript.

No todos los principios demostrados deben seguirse estrictamente, y aún menos son universalmente aceptados. Estos principios son solo directrices y nada más, sin embargo, han sido codificados a través de muchos años de experiencia colectiva por los autores de Clean Code.

Nuestro oficio de ingeniería de software tiene poco más de 50 años, y aún estamos aprendiendo mucho. Cuando la arquitectura de software tenga la misma antigüedad que la arquitectura de edificios, quizás entonces tendremos reglas más estrictas a seguir. Por ahora, deja que estas directrices sirvan como criterio para evaluar la calidad del código JavaScript que tú y tu equipo produzcan.

Una cosa más: aprender esto no te convertirá instantáneamente en un mejor desarrollador de software, y trabajar con estos principios durante muchos años no significa que no cometerás errores. Cada porción de código comienza como un borrador, como arcilla húmeda moldeada en su forma final. Finalmente, esculpimos las imperfecciones cuando revisamos con nuestros colegas. No te sientas culpable por los primeros borradores que aún necesitan mejoras. En cambio, desquita en tu código.

## **Variables**

### Usa nombres descriptivos y pronunciables para las variables

**Malo:**
```java
String a = "2024-09-15";
```

**Bueno:**
```java
String currentDate = "2024-09-15";
```

### Usa el estándar camelCase para los nombres de variables y métodos

**Malo:**
```java
String Current_Date = "2024-09-15";
```

**Bueno:**
```java
String currentDate = "2024-09-15";
```

### Evita nombres innecesariamente complejos para las variables

**Malo:**
```java
int wxyz = calculate();
```

**Bueno:**
```java
int totalCost = calculate();
```

### Usa constantes para valores "mágicos"

**Malo:**
```java
if (user.age > 18) {
    // código
}
```

**Bueno:**
```java
private static final int ADULT_AGE = 18;

if (user.age > ADULT_AGE) {
    // código
}
```

## **Métodos**

### Mantén los métodos cortos y enfocados en una sola tarea

**Malo:**
```java
public void saveUser(User user) {
    validateUser(user);
    logUserSaveAttempt(user);
    database.save(user);
    emailService.sendConfirmation(user);
}
```

**Bueno:**
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

### Usa nombres descriptivos para los métodos

**Malo:**
```java
public void handle() {
    // código
}
```

**Bueno:**
```java
public void processUserRegistration() {
    // código
}
```

### Evita métodos con demasiados parámetros

**Malo:**
```java
public void createUser(String name, String email, int age, String address, String phone) {
    // código
}
```

**Bueno:**
```java
public void createUser(UserDTO userDTO) {
    // código
}
```

## **Objetos y Estructuras de Datos**

### Evita exponer detalles internos de los objetos

**Malo:**
```java
public class User {
    public String name;
    public String email;
}
```

**Bueno:**
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

## **Clases**

### Aplica el Principio de Responsabilidad Única

Cada clase debería tener una única responsabilidad o propósito. Divide clases grandes y complejas en clases más pequeñas.

**Malo:**
```java
public class UserService {
    public void createUser() { /* lógica de creación */ }
    public void sendWelcomeEmail() { /* lógica de envío de correo */ }
    public void validateUser() { /* lógica de validación */ }
}
```

**Bueno:**
```java
public class UserService {
    public void createUser() { /* lógica de creación */ }
}

public class EmailService {
    public void sendWelcomeEmail() { /* lógica de envío de correo */ }
}

public class UserValidator {
    public void validateUser() { /* lógica de validación */ }
}
```

## **SOLID**
Aplica los principios SOLID:
- **S**: Principio de Responsabilidad Única
- **O**: Principio de Abierto/Cerrado
- **L**: Principio de Sustitución de Liskov
- **I**: Principio de Segregación de Interfaces
- **D**: Principio de Inversión de Dependencias

**Ejemplo de aplicación del OCP (Principio de Abierto/Cerrado):**

**Malo:**
```java
public class Invoice {
    public double calculateTotal() {
        // lógica de cálculo
    }
}
```

**Bueno:**
```java
public interface Invoice {
    double calculateTotal();
}

public class RegularInvoice implements Invoice {
    @Override
    public double calculateTotal() {
        // lógica de cálculo
    }
}

public class DiscountedInvoice implements Invoice {
    @Override
    public double calculateTotal() {
        // lógica de cálculo con descuento
    }
}
```

## **Manejo de Excepciones**

### No ignores las excepciones

**Malo:**
```java
try {
    // código
} catch (Exception e) {
    // no hace nada
}
```

**Bueno:**
```java
try {
    // código
} catch (Exception e) {
    log.error("Error al ejecutar la operación", e);
}
```
---
## **Traduções**

Existen traducciones disponibles en otros idiomas:

- ![br](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Brazil.png) **Português**: [Boas práticas de código limpo em Java](https://github.com/williamsartijose/clean-code-java/blob/main/README/README_BR.md)
- ![en](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/United-States.png) **English**: [Clean Code Best Practices in Java](https://github.com/williamsartijose/clean-code-java/blob/main/README/README_EN.md)
- ![es](https://github.com/gosquared/flags/blob/master/src/flags/Spain/24.png) **Español**: [Buenas prácticas de código limpio en Java](https://github.com/williamsartijose/clean-code-java/blob/main/README/README_ES.md)




---
