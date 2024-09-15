
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

![Imagem humorística da estimativa de qualidade do software baseado na contagem de quantos palavrões você gritou enquanto lia o código.](http://www.osnews.com/images/comics/wtfm.jpg)

Princípios da Engenharia de Software, do livro de Robert C. Martin
[*Código Limpo*](https://www.amazon.com.br/C%C3%B3digo-Limpo-Habilidades-Pr%C3%A1ticas-Software/dp/8576082675),
adaptados para Java. Isto não é um guia de estilos. É um guia para se produzir código [legível, reutilizável e refatorável](https://github.com/ryanmcdermott/3rs-of-software-architecture) em Java.

Nem todo princípio demonstrado deve ser seguido rigorosamente, e ainda menos são um consenso universal. Estes princípios são orientações e nada mais, entretanto, foram codificados durante muitos anos de experiência coletiva pelos autores de *Código limpo*.

Nosso ofício de engenharia de software tem pouco mais de 50 anos e ainda estamos aprendendo muito. Quando a arquitetura de software for tão velha quanto a própria arquitetura, talvez então tenhamos regras mais rígidas para seguir. Por enquanto, deixe que estas orientações sirvam como critério para se avaliar a qualidade de código Java que tanto você e o seu time produzirem.

Mais uma coisa: aprender isto não irá lhe transformar imediatamente em um desenvolvedor de software melhor, trabalhar com eles por muitos anos não quer dizer que você não cometerá erros. Toda porção de código começa com um rascunho, como argila molhada sendo moldada em sua forma final. Finalmente, talhamos as imperfeições quando revisamos com nossos colegas. Não se sinta culpado pelos primeiros rascunhos que ainda precisam de melhorias. Ao invés, desconte em seu código.

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

- ![br](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Brazil.png) **Português**: [Boas práticas de código limpo em Java](https://github.com/williamsartijose/clean-code-java/blob/main/README/README_BR.md)
- ![en](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/United-States.png) **English**: [Clean Code Best Practices in Java](https://github.com/williamsartijose/clean-code-java/blob/main/README/README_EN.md)
- ![es](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Uruguay.png) **Español**: [Buenas prácticas de código limpio en Java](https://github.com/williamsartijose/clean-code-java/blob/main/README/README_ES.md)


---
