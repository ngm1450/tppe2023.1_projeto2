# Simplicidade

## 1. Introdução

A simplicidade é um dos princípios fundamentais do desenvolvimento de software. Segundo Martin Fowler em seu livro "Refactoring: Improving the Design of Existing Code" (FOWLER, 1999), a simplicidade pode ser considerada a arte de maximizar a quantidade de trabalho não realizado. É a ideia de tornar o código facilmente compreensível e direto. No entanto, a simplicidade é frequentemente um conceito subjetivo que pode variar de acordo com a experiência do desenvolvedor, as práticas de codificação utilizadas e o contexto específico de um projeto de software.

Kent Beck, em "Extreme Programming Explained: Embrace Change" (BECK, 2000), argumenta que a simplicidade não deve ser vista apenas como a ausência de complexidade, mas sim como algo ativamente perseguido. Simplificar o código não significa apenas remover partes desnecessárias, mas organizar e estruturar o código de uma maneira que seja fácil de entender e modificar. Isso muitas vezes requer um profundo entendimento do problema a ser resolvido e do domínio do problema.

## 2. Relação com os maus-cheiros de código

Os maus-cheiros de código são sinais de que o código pode precisar ser refatorado. A falta de simplicidade é um dos principais maus-cheiros. Por exemplo, os "métodos longos" (Long Methods) são geralmente mais difíceis de entender e manter, pois contêm muitas linhas de código e, muitas vezes, várias responsabilidades.

Outro mau-cheiro de código relacionado à falta de simplicidade é o "código duplicado" (Duplicated Code). Quando o mesmo código é repetido em vários lugares, isso pode indicar uma falta de simplicidade, pois uma mudança em uma parte do código precisará ser repetida em todos os lugares onde o código é duplicado. Isso torna o código mais difícil de manter e pode levar a erros se as mudanças não forem feitas de maneira consistente.

## 3. Operação de refatoração

A refatoração é uma prática que ajuda a tornar o código mais simples. Para resolver o mau-cheiro de "métodos longos", a operação de refatoração chamada "Extrair Método" (Extract Method) pode ser usada. Isso envolve dividir o método em vários métodos menores, cada um com uma responsabilidade clara. Isso torna o código mais fácil de entender, pois cada método realiza uma tarefa específica e o código geral torna-se mais modular.

Para lidar com o "código duplicado", a operação de refatoração chamada "Extrair Método" (Extract Method) também pode ser usada, ou mesmo a "Form Template Method". Ambas envolvem a criação de um novo método que contém o código duplicado. Este método é então chamado onde quer que o código seja necessário, reduzindo a duplicação e tornando o código mais simples e fácil de manter.

## 4. Exemplos

### 4.1 Extrair Método (Extract Method)

Considere o seguinte código Java que exemplifica um "método longo":

```java
public double calculateTotal() {
    double itemTotal = 0;
    for (Item item : items) {
        itemTotal += item.getPrice() * item.getQuantity();
    }
    double discount = 0;
    if (customer.isPreferred()) {
        discount = itemTotal * 0.05;
    }
    double tax = (itemTotal - discount) * 0.06;
    return itemTotal - discount + tax;
}

```

Usando a refatoração "Extrair Método", o código acima pode ser simplificado como:

```java

public double calculateTotal() {
    double itemTotal = calculateItemTotal();
    double discount = calculateDiscount(itemTotal);
    double tax = calculateTax(itemTotal, discount);
    return itemTotal - discount + tax;
}

public double calculateItemTotal() {
    double itemTotal = 0;
    for (Item item : items) {
        itemTotal += item.getPrice() * item.getQuantity();
    }
    return itemTotal;
}

public double calculateDiscount(double itemTotal) {
    if (customer.isPreferred()) {
        return itemTotal * 0.05;
    }
    return 0;
}

public double calculateTax(double itemTotal, double discount) {
    return (itemTotal - discount) * 0.06;
}
```

### 4.1 Extract Superclass (Extrair Superclasse)

Para o problema de "duplicated code", uma operação de refatoração comum usada é a "Extract Method", semelhante ao que fizemos acima. No entanto, para lidar melhor com a duplicação de código, especialmente quando o mesmo ocorre em várias partes do código ou entre classes diferentes, podemos usar a técnica de refatoração "Extract Superclass" ou "Extract Class".

Considere que você tenha duas classes diferentes que compartilham código semelhante para calcular descontos:

```java
public class OnlineOrder {
    // ...
    public double calculateDiscount() {
        double discount = 0;
        if (customer.isPreferred()) {
            discount = subtotal * 0.1;
        }
        return discount;
    }
}

public class InStoreOrder {
    // ...
    public double calculateDiscount() {
        double discount = 0;
        if (customer.isPreferred()) {
            discount = subtotal * 0.1;
        }
        return discount;
    }
}
```

Neste caso, estamos repetindo o mesmo código em duas classes diferentes. Uma maneira de refatorar isso seria extrair a lógica de desconto para uma classe pai ou para uma nova classe:

```java

public class Order {
    // ...
    public double calculateDiscount() {
        double discount = 0;
        if (customer.isPreferred()) {
            discount = subtotal * 0.1;
        }
        return discount;
    }
}

public class OnlineOrder extends Order {
    // ...
}

public class InStoreOrder extends Order {
    // ...
}


```

Agora, ambas `OnlineOrder` e `InStoreOrder` herdam o método `calculateDiscount()` de `Order`, eliminando a duplicação de código.

## 5. Referências

Fowler, M. (1999). Refactoring: Improving the Design of Existing Code. Addison-Wesley.

Beck, K. (2000). Extreme Programming Explained: Embrace Change. Addison-Wesley.
