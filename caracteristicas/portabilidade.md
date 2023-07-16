# Portabilidade

## 1. Introdução

Portabilidade, no contexto de desenvolvimento de software, refere-se à facilidade com que um programa de computador pode ser executado em diferentes ambientes de computação. Uma das principais vantagens de ter um código portátil é que ele pode ser executado em vários sistemas operacionais e dispositivos sem a necessidade de modificações substanciais (Seacord, R., 2013). Em termos de efeitos no código, isso pode envolver a seleção cuidadosa de bibliotecas e ferramentas, aderência aos padrões da indústria e a abstração de funcionalidades específicas da plataforma.

Entretanto, a portabilidade pode aumentar a complexidade do código, pois envolve lidar com variações entre plataformas. Para controlar essa complexidade, as abstrações apropriadas devem ser utilizadas para separar o código específico da plataforma do restante do programa, aumentando a coesão e reduzindo o acoplamento (Hannay, J.E., et al, 2009).

## 2. Relação com os maus-cheiros de código

A "Dependência de plataforma" é um exemplo claro de mau cheiro que afeta a portabilidade. Esse mau cheiro ocorre quando o código depende de características específicas de uma plataforma, tornando-o difícil de portar para outra. 

Outro mau-cheiro relacionado à portabilidade é o "Código duplicado". Quando o código é copiado e colado com pequenas alterações para lidar com diferentes plataformas, ele se torna difícil de manter e de portar para novas plataformas.

## 3. Operação de refatoração

Uma operação de refatoração que pode ajudar a lidar com a "Dependência de plataforma" é a "Abstração de plataforma". Esta operação envolve a criação de uma interface comum que pode ser implementada de maneira diferente para cada plataforma suportada. 

Outra operação de refatoração que pode lidar com problemas de portabilidade é a "Parametrização". Esse método de refatoração envolve passar um objeto ou valor primitivo como parâmetro para um método, em vez de ter o método buscar diretamente o recurso. Isso ajuda a tornar o código mais portátil, pois o mesmo método pode ser usado em diferentes contextos ou plataformas, apenas variando os parâmetros.

## 4. Exemplos

### 4.1 Abstração de plataforma (Plataform abstraction)

Para ilustrar a dependência da plataforma, vamos considerar um exemplo em que uma operação de escrita de arquivo é feita de maneiras diferentes, dependendo do sistema operacional. Esse é um código que possui um mau cheiro de "Dependência de plataforma", pois depende de características específicas de uma plataforma.

```java
void writeFile(String content) {
    if (System.getProperty("os.name").startsWith("Windows")) {
        // Write file in Windows
    } else {
        // Write file in Unix/Linux
    }
}
```

A refatoração que pode resolver essa questão é a "Abstração de plataforma". Podemos definir uma interface FileWriter que tem um método writeFile. Então, para cada plataforma que queremos suportar, implementamos a interface com as especificidades daquela plataforma.

```java
interface FileWriter {
    void writeFile(String content);
}

class WindowsFileWriter implements FileWriter {
    @Override
    public void writeFile(String content) {
        // Write file in Windows
    }
}

class UnixFileWriter implements FileWriter {
    @Override
    public void writeFile(String content) {
        // Write file in Unix/Linux
    }
}
```

### 4.2 Parametrização (Plataform abstraction)

Considere um exemplo de um método que está usando um caminho de arquivo hardcoded:

```java
void readData() {
    File file = new File("/hardcoded/path/to/data.txt");
    // Read and process data
}
```

Este código não é portátil pois assume um caminho de arquivo específico que pode não existir ou pode ser diferente em outras plataformas ou ambientes.

Podemos refatorar esse código usando a técnica de "Parametrização". Passamos o caminho do arquivo como um parâmetro para o método readData, permitindo que ele seja usado de maneira mais flexível em diferentes ambientes:


```java
void readData(String filePath) {
    File file = new File(filePath);
    // Read and process data
}
```

Dessa forma, tornamos o código mais portátil e flexível, pois podemos fornecer o caminho do arquivo correto dependendo do ambiente em que o software está sendo executado.







## 5. Referências
Seacord, R. (2013). "Secure Coding in C and C++ (2nd Edition)". Addison-Wesley.

Hannay, J. E., Dybå, T., Arisholm, E., & Sjøberg, D. I. (2009). The effectiveness of pair programming: A meta-analysis. "Information and Software Technology", 51(7), 1110-1122.