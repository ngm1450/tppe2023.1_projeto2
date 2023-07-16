# Elegância

## 1. Introdução

Elegância, em termos de codificação, refere-se à arte de escrever código que é fácil de ler, entender e manter. Código elegante muitas vezes parece simples e direto, apesar de resolver problemas complexos ou desafiadores. McConnell (2004) sugere que a elegância é alcançada ao se equilibrar entre a simplicidade e a funcionalidade do código, um código elegante não sacrifica a eficácia em nome da simplicidade, e vice-versa.

A elegância também influencia significativamente a estrutura do código. De acordo com Martin (2008), um código elegante promove uma estrutura limpa, modular e coesa, facilitando a compreensão do fluxo lógico do programa. Isso leva a um acoplamento mais baixo e a um código mais fácil de manter e estender.

## 2. Relação com os maus-cheiros de código

Dois maus-cheiros de código comumente associados a falta de elegância são "Código Duplicado" e "Complexidade desnecessária". Código duplicado pode tornar o código confuso e difícil de manter, pois qualquer alteração precisa ser feita em vários lugares. Por outro lado, a complexidade desnecessária pode tornar o código difícil de entender e estender, pois há mais elementos para se preocupar do que o necessário.

## 3. Operação de refatoração

Para lidar com o mau-cheiro de código "Código Duplicado", a refatoração "Extrair Método" é frequentemente usada. Essa técnica envolve identificar o código duplicado, movê-lo para um novo método e substituir o código duplicado original por chamadas ao novo método. Isso torna o código mais elegante, pois remove a repetição e torna o código mais fácil de entender e manter.

Por outro lado, para lidar com o mau-cheiro "Complexidade desnecessária", a refatoração "Substituir código por dados" pode ser aplicada. Isso envolve identificar partes do código que podem ser substituídas por estruturas de dados ou objetos simples. Isso simplifica o código, removendo elementos desnecessários e tornando-o mais fácil de entender.

## 4. Exemplos

### 4.1 Extrair Método (Extract Method)

```java
// Antes
public void printReceipt() {
    // Print header
    System.out.println("Company Name");
    System.out.println("Address");

    // Print details...

    // Print footer
    System.out.println("Company Name");
    System.out.println("Address");
}

// Depois
public void printReceipt() {
    printHeader();
    // Print details...
    printFooter();
}

private void printHeader() {
    System.out.println("Company Name");
    System.out.println("Address");
}

private void printFooter() {
    System.out.println("Company Name");
    System.out.println("Address");
}
```

### 4.1 Substituir código por dados

```java
// Antes
public class User {
    private String type;

    public boolean isAdmin() {
        return type.equals("ADMIN");
    }

    public boolean isModerator() {
        return type.equals("MODERATOR");
    }

    public boolean isUser() {
        return type.equals("USER");
    }
}

// Depois
public class User {
    private UserType type;

    public boolean isAdmin() {
        return type == UserType.ADMIN;
    }

    public boolean isModerator() {
        return type == UserType.MODERATOR;
    }

    public boolean isUser() {
        return type == UserType.USER;
    }
}

public enum UserType {
    ADMIN,
    MODERATOR,
    USER
}
```

## 5. Referências

McConnell, S. (2004). Code Complete: A Practical Handbook of Software Construction, Second Edition. Microsoft Press.

Martin, R. C. (2008). Clean Code: A Handbook of Agile Software Craftsmanship. Prentice Hall.
