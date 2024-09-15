
# clean-code-java

## Índice
  1. [Introdução](#introdução)
  2. [Variáveis](#variáveis)
  3. [Métodos](#métodos)
  4. [Objetos e Estruturas de Dados](#objetos-e-estruturas-de-dados)
  5. [Classes](#classes)
  6. [SOLID](#solid)
  7. [Testes](#testes)
  8. [Concorrência](#concorrência)
  9. [Tratamento de Exceções](#tratamento-de-exceções)
  10. [Formatação](#formatação)
  11. [Comentários](#comentários)
  12. [Traduções](#traduções)

## Introdução
Princípios da Engenharia de Software do livro de Robert C. Martin, *Código Limpo*, adaptados para Java. Estes princípios ajudam a escrever código legível, reutilizável e fácil de manter. 

Embora sejam diretrizes importantes, não são regras imutáveis. Elas devem guiar o desenvolvimento e ajudar na construção de código mais limpo e sustentável.

## **Variáveis**

### Use nomes de variáveis descritivos e pronunciáveis

**Ruim:**
```java
String a = "2024-09-15";
```

**Bom:**
```java
String currentDate = "2024-09-15";
```

### Use o padrão camelCase para nomes de variáveis e métodos

**Ruim:**
```java
String Current_Date = "2024-09-15";
```

**Bom:**
```java
String currentDate = "2024-09-15";
```

### Evite nomes de variáveis desnecessariamente complexos

**Ruim:**
```java
int wxyz = calculate();
```

**Bom:**
```java
int totalCost = calculate();
```

### Use constantes para valores "mágicos"

**Ruim:**
```java
if (user.age > 18) {
    // código
}
```

**Bom:**
```java
private static final int ADULT_AGE = 18;

if (user.age > ADULT_AGE) {
    // código
}
```

## **Métodos**

### Mantenha os métodos curtos e focados em uma única tarefa

**Ruim:**
```java
public void saveUser(User user) {
    validateUser(user);
    logUserSaveAttempt(user);
    database.save(user);
    emailService.sendConfirmation(user);
}
```

**Bom:**
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

### Use nomes descritivos para métodos

**Ruim:**
```java
public void handle() {
    // código
}
```

**Bom:**
```java
public void processUserRegistration() {
    // código
}
```

### Evite métodos com muitos parâmetros

**Ruim:**
```java
public void createUser(String name, String email, int age, String address, String phone) {
    // código
}
```

**Bom:**
```java
public void createUser(UserDTO userDTO) {
    // código
}
```

## **Objetos e Estruturas de Dados**

### Evite expor os detalhes internos dos objetos

**Ruim:**
```java
public class User {
    public String name;
    public String email;
}
```

**Bom:**
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

### Aplique o princípio da responsabilidade única

Cada classe deve ter uma única responsabilidade ou propósito. Divida classes grandes e complexas em classes menores.

**Ruim:**
```java
public class UserService {
    public void createUser() { /* lógica de criação */ }
    public void sendWelcomeEmail() { /* lógica de envio de e-mail */ }
    public void validateUser() { /* lógica de validação */ }
}
```

**Bom:**
```java
public class UserService {
    public void createUser() { /* lógica de criação */ }
}

public class EmailService {
    public void sendWelcomeEmail() { /* lógica de envio de e-mail */ }
}

public class UserValidator {
    public void validateUser() { /* lógica de validação */ }
}
```

## **SOLID**
Aplique os princípios SOLID:
- **S**: Princípio da responsabilidade única
- **O**: Princípio do aberto-fechado
- **L**: Princípio da substituição de Liskov
- **I**: Princípio da segregação de interfaces
- **D**: Princípio da inversão de dependência

**Exemplo de aplicação do OCP (Open-Closed Principle):**

**Ruim:**
```java
public class Invoice {
    public double calculateTotal() {
        // lógica de cálculo
    }
}
```

**Bom:**
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
        // lógica de cálculo com desconto
    }
}
```

## **Tratamento de Exceções**

### Não ignore exceções

**Ruim:**
```java
try {
    // código
} catch (Exception e) {
    // não faz nada
}
```

**Bom:**
```java
try {
    // código
} catch (Exception e) {
    log.error("Erro ao executar operação", e);
}
```
---
## **Traduções**

Existem traduções disponíveis em outras línguas:

  - ![en](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/United-States.png) **Inglês**: [ryanmcdermott/clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript)
  - ![es](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Uruguay.png) **Espanhol**: [andersontr15/clean-code-javascript](https://github.com/andersontr15/clean-code-javascript-es)
  - ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Chinês**:
    - [alivebao/clean-code-js](https://github.com/alivebao/clean-code-js)
    - [beginor/clean-code-javascript](https://github.com/beginor/clean-code-javascript)
  - ![de](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Germany.png) **Alemão**: [marcbruederlin/clean-code-javascript](https://github.com/marcbruederlin/clean-code-javascript)
  - ![kr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/South-Korea.png) **Coreano**: [qkraudghgh/clean-code-javascript-ko](https://github.com/qkraudghgh/clean-code-javascript-ko)
  - ![pl](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Poland.png) **Polonês**: [greg-dev/clean-code-javascript-pl](https://github.com/greg-dev/clean-code-javascript-pl)
  - ![ru](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Russia.png) **Russo**:
    - [BoryaMogila/clean-code-javascript-ru/](https://github.com/BoryaMogila/clean-code-javascript-ru/)
    - [maksugr/clean-code-javascript](https://github.com/maksugr/clean-code-javascript)
  - ![vi](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Vietnam.png) **Vietnamita**: [hienvd/clean-code-javascript/](https://github.com/hienvd/clean-code-javascript/)
  - ![ja](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Japan.png) **Japonês**: [mitsuruog/clean-code-javascript/](https://github.com/mitsuruog/clean-code-javascript/)
  - ![id](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Indonesia.png) **Indonésio**:
  [andirkh/clean-code-javascript/](https://github.com/andirkh/clean-code-javascript/)

---