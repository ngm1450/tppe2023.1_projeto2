# Boas Interfaces

## 1. Introdução

Boas interfaces de software, no contexto da programação orientada a objetos, referem-se a interfaces claras, consistentes e intuitivas que expõem a funcionalidade de um objeto ou módulo de maneira lógica e coerente. A importância de boas interfaces pode ser resumida pela frase de Joshua Bloch: "Quando estou a trabalhar em um problema, eu nunca penso sobre beleza. Eu apenas penso sobre como resolver o problema. Mas quando eu termino, se a solução não é bonita, eu sei que está errada" (Bloch, 2006, p. 45). Além disso, Robert C. Martin em seu livro "Clean Code" afirma que "Uma classe não deve saber sobre as coisas de que não precisa. Um módulo deve saber o mínimo sobre o sistema" (Martin, 2008, p.97). Isso implica que uma boa interface esconde a complexidade e permite que outras partes do sistema interajam com ela sem conhecer os detalhes de implementação.

## 2. Relação com os maus-cheiros de código

Boas interfaces podem ajudar a prevenir muitos maus-cheiros de código. Um exemplo é o "Inappropriate Intimacy", onde um módulo conhece e depende fortemente dos detalhes internos de outro módulo. Isso é contrário ao princípio de boas interfaces e pode ser evitado ao se projetar interfaces bem definidas que ocultem os detalhes de implementação. 

Outro mau-cheiro é "Shotgun Surgery", que ocorre quando uma mudança em uma parte do sistema exige muitas pequenas alterações em muitas outras partes do sistema. Se as interfaces do sistema forem bem projetas, tais mudanças serão limitadas a uma ou duas classes ou módulos.

## 3. Operação de refatoração

O mau-cheiro "Inappropriate Intimacy" pode ser tratado através da operação de refatoração "Move Method" ou "Move Field", para mover a lógica ou dados para o módulo apropriado e reduzir o acoplamento. 

Para "Shotgun Surgery", a operação de refatoração "Extract Class" pode ser útil, onde se cria uma nova classe para agrupar as funcionalidades relacionadas e expô-las através de uma interface limpa e coerente.

## 4. Exemplos

### 4.1 Mover Método (Move Method)

Para o mau-cheiro "Inappropriate Intimacy", considere a seguinte classe Java:

```java
public class Order {
    Customer customer;
    // Other fields...

    public String getCustomerName() {
        return customer.getName();
    }
}
```

A classe Order possui um método  `getCustomerName()` que estava buscando o nome do cliente. O problema aqui é que `Order` estava muito intimamente acoplado a `Customer`, sabendo e dependendo de detalhes internos de `Customer`. Isso é um exemplo do mau-cheiro de código "Inappropriate Intimacy".

A refatoração "Move Method" foi usada para tratar esse problema. O método getCustomerName() foi movido de Order para Customer. Isso reduz o acoplamento entre as duas classes, pois Order não precisa mais conhecer os detalhes internos de Customer.

Após a refatoração, a classe Order se torna:

```java
public class Order {
    Customer customer;
    // Outros campos...
}
```
E uma nova implementação do método getName() é adicionada à classe Customer:

```java
public class Customer {
    // Outros campos...

    public String getName() {
        // Implementação...
    }
}
```
### 4.1 Extrair Classe (Extract Class)

Para o mau-cheiro "Shotgun Surgery", considere a seguinte classe Java:

```java
public class OrderProcessor {
    public void process(Order order) {
        // Validate order...
        // Calculate total price...
        // Apply discounts...
        // Other order processing steps...
    }
}
```

A classe OrderProcessor tinha um único método, process(), que realizava várias funções diferentes, incluindo a validação do pedido, o cálculo do preço total e a aplicação de descontos. O problema aqui é que qualquer mudança em um desses aspectos do processamento do pedido exigiria alterações na classe OrderProcessor. Isso é um exemplo do mau-cheiro de código "Shotgun Surgery".

A refatoração "Extract Class" foi usada para tratar esse problema. Cada função do método process() foi extraída para sua própria classe. Isso resultou em várias novas classes, cada uma com uma única responsabilidade.

Após a refatoração, a classe OrderProcessor se torna:

```java
public class OrderProcessor {
    public void process(Order order) {
        OrderValidator.validate(order);
        PricingCalculator.calculate(order);
        DiscountApplier.apply(order);
        // Outros passos de processamento de pedido...
    }
}
```

E novas classes são criadas para cada função:

```java
public class OrderValidator {
    public static void validate(Order order) {
        // Valida o pedido...
    }
}

public class PricingCalculator {
    public static void calculate(Order order) {
        // Calcula o preço total...
    }
}

public class DiscountApplier {
    public static void apply(Order order) {
        // Aplica descontos...
    }
}
```

Cada uma dessas novas classes agora tem uma única responsabilidade e a classe OrderProcessor não precisa mais se preocupar com os detalhes de como cada uma dessas funções é implementada. Isso faz com que futuras mudanças em qualquer uma dessas funções sejam mais fáceis, pois serão limitadas à classe responsável por essa função.