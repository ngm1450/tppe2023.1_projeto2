# Extensibilidade

## 1. Introdução

A extensibilidade é uma característica desejável do software que permite a adição de novas funcionalidades ou modificações das existentes com esforço mínimo e sem afetar outras partes do sistema. Um sistema extensível é projetado de maneira que seja fácil de compreender, modificar e ampliar (Pressman, R.S. et al., 2014). Essa característica tem impactos diretos na estrutura do código, uma vez que exige um design modular e organizado, facilitando a clareza e a coesão. Além disso, a extensibilidade minimiza o acoplamento entre módulos, tornando-os independentes e permitindo modificações individuais.

No entanto, a extensibilidade não é apenas uma questão de design. Ela também envolve uma abordagem disciplinada para a programação e uma compreensão das melhores práticas de desenvolvimento de software. A extensibilidade é também uma maneira de preparar o software para a inevitável mudança, uma vez que os requisitos de software raramente permanecem estáticos ao longo do tempo (Sommerville, I., 2015).

## 2. Relação com os maus-cheiros de código

Os "maus-cheiros de código", como definidos por Fowler, são sinais de que o código pode precisar de refatoração. Alguns maus-cheiros podem indicar problemas com a extensibilidade do código. Por exemplo, "Classes God" que têm muita responsabilidade podem dificultar a extensibilidade, pois a adição de novas funcionalidades pode exigir alterações significativas na classe.

Outro mau-cheiro relacionado à extensibilidade é a "Rigidez do Software", que se refere à dificuldade de mudar o software porque qualquer alteração afeta muitas outras partes do sistema. Um software rígido é o oposto de um software extensível, pois não permite que novas funcionalidades sejam adicionadas facilmente.

## 3. Operação de refatoração

Para combater a "Classe God", uma operação de refatoração útil é a "Extração de Classe". Esta técnica envolve mover responsabilidades excessivas de uma classe para uma ou mais novas classes. Isso pode tornar o sistema mais extensível, pois facilita a adição de novas funcionalidades a estas novas classes menores e mais focadas.

Em relação à "Rigidez do Software", uma refatoração útil é a "Modularização", que já foi discutida anteriormente. Ao dividir o software em módulos independentes, é mais fácil adicionar funcionalidades a um módulo específico sem afetar os outros.

## 4. Exemplos

### 4.1 Extração de Classe (Class extraction)

Considere uma classe `Vehicle` que tenha responsabilidades excessivas, incluindo métodos para dirigir, reabastecer, tocar música, acender as luzes, etc. Isso pode tornar difícil a adição de novas funcionalidades à classe `Vehicle`.

```java
class Vehicle {
    void drive() { /* ... */ }
    void refuel() { /* ... */ }
    void playMusic() { /* ... */ }
    void turnOnLights() { /* ... */ }
}
```

Através da "Extração de Classe", podemos mover algumas dessas responsabilidades para novas classes, como `Radio` e `Headlights`. Isso torna o sistema mais extensível, pois podemos adicionar novas funcionalidades a essas classes menores.

```java
class Vehicle {
    Radio radio = new Radio();
    Headlights headlights = new Headlights();

    void drive() { /* ... */ }
    void refuel() { /* ... */ }
}

class Radio {
    void playMusic() { /* ... */ }
}

class Headlights {
    void turnOnLights() { /* ... */ }
}
```

## 5. Referências

Pressman, R. S., Maxim, B. R. (2014). Engenharia de Software: Uma Abordagem Profissional. Porto Alegre: AMGH.

Sommerville, I. (2015). Engenharia de Software. Porto Alegre: Pearson.