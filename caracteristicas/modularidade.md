# Modularidade

## 1. Descrição
A modularidade refere-se à prática de dividir um sistema de software em módulos distintos e independentes, que podem ser desenvolvidos, testados, compreendidos e modificados de forma independente (Parnas, 1972). Esta abordagem promove a coesão, já que cada módulo tem uma única responsabilidade bem definida, e reduz o acoplamento, pois cada módulo interage com os outros através de interfaces bem definidas.

De acordo com Robert C. Martin em seu livro "Clean Code: A Handbook of Agile Software Craftsmanship" (2008), um sistema modularizado tem maior capacidade de suportar mudanças, uma vez que a modificação em um módulo tem pouco ou nenhum impacto nos outros. Além disso, a modularidade aumenta a legibilidade e a compreensibilidade do código, facilitando o processo de manutenção e extensão do software.

## 2. Relação com os maus-cheiros de código
Maus-cheiros como "Large Class" e "God Class" são indicativos de falta de modularidade. Classes muito grandes ou com muitas responsabilidades dificultam a manutenção, a compreensão e o teste do código.

Outro mau-cheiro, "Inappropriate Intimacy", também se opõe à modularidade. Este ocorre quando uma classe usa internamente detalhes de implementação de outra classe, violando o princípio de encapsulamento e tornando os módulos excessivamente acoplados.

## 3. Operação de refatoração
A refatoração "Extract Class" pode ser aplicada para lidar com "Large Class" ou "God Class". Esta operação envolve a identificação de responsabilidades que podem ser agrupadas em uma nova classe, aumentando assim a modularidade do código.

Para o mau-cheiro "Inappropriate Intimacy", a refatoração "Move Method" ou "Move Field" pode ser utilizada. Essas operações permitem mover métodos ou campos para a classe apropriada, reduzindo o acoplamento entre classes e melhorando a modularidade.

## 4. Exemplos

### 4.1 Extract Class (Extrair Classe)

Suponha que temos uma classe `Customer` que também é responsável por gerar relatórios do cliente.

```java
public class Customer {
    private String name;
    private List<Order> orders;
    // ... outros campos

    // Métodos relacionados ao cliente
    public void addOrder(Order order) {
        // ...
    }

    // Métodos de geração de relatório
    public String generateReport() {
        // ...
    }
}

```

 Podemos aplicar a refatoração "Extract Class" para separar as responsabilidades de geração de relatórios para uma nova classe `CustomerReport`. 

 ```java
 public class Customer {
    private String name;
    private List<Order> orders;
    // ... outros campos

    // Métodos relacionados ao cliente
    public void addOrder(Order order) {
        // ...
    }
}

public class CustomerReport {
    private Customer customer;

    public CustomerReport(Customer customer) {
        this.customer = customer;
    }

    // Métodos de geração de relatório movidos para esta classe
    public String generateReport() {
        // ...
    }
}

 ```


### 4.2 Move Field (Mover Campo)

Em outro cenário, se a classe `Order` está usando diretamente campos de `Customer`, isto é:

 ```java
public class Customer {
    private String name;
    private List<Order> orders;
    public int discount; // campo usado por Order

    // ...
}

public class Order {
    private Customer customer;

    public double calculatePrice() {
        double price = // ...
        price -= price * customer.discount / 100.0;
        return price;
    }
}

 ```


podemos aplicar a refatoração "Move Field" para mover os campos apropriados para a classe `Order`, melhorando o encapsulamento e a modularidade.

 ```java
public class Customer {
    private String name;
    private List<Order> orders;
    // campo discount movido para Order

    // ...
}

public class Order {
    private Customer customer;
    private int discount; // campo movido para cá

    public double calculatePrice() {
        double price = // ...
        price -= price * discount / 100.0;
        return price;
    }
}
 ```



## 5. Referências
Martin, R. C. (2008). Clean Code: A Handbook of Agile Software Craftsmanship. Prentice Hall.

Parnas, D. L. (1972). On the Criteria To Be Used in Decomposing Systems into Modules. Communications of the ACM, 15(12), 1053-1058.
