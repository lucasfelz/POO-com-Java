# Projetando Classes em Java

## Visão Geral

Este documento aborda conceitos fundamentais de programação orientada a objetos (POO) em Java, incluindo instanciação de objetos, coesão, acoplamento e organização de código através de pacotes.

## Objetos

### Conceitos Básicos

Uma **classe** é uma estrutura que define propriedades (atributos) e comportamentos (métodos) que objetos podem ter. Funciona como um modelo para criação de objetos.

**Objetos** são instâncias reais de uma classe que existem em tempo de execução, possuem estado (valores de atributos) e podem realizar ações (invocar métodos).

### Instanciação de Objetos

#### Definição da Classe
```java
public class Carro {
    private String marca;
    private String modelo;
    
    public Carro(String marca, String modelo) {
        this.marca = marca;
        this.modelo = modelo;
    }
    
    public String getMarca() {
        return marca;
    }
    
    public void setMarca(String marca) {
        this.marca = marca;
    }
    
    // Outros métodos...
}
```

#### Criação de Instância
```java
Carro meuCarro = new Carro("Toyota", "Corolla");
```

### Acesso a Membros

#### Atributos Públicos
```java
meuCarro.marca = "Toyota";  // Acesso direto (não recomendado)
```

#### Atributos Privados (Recomendado)
```java
meuCarro.setMarca("Toyota");
String marca = meuCarro.getMarca();
```

#### Métodos
```java
meuCarro.acelerar();
meuCarro.ligarMotor(2000);  // Com parâmetros
```

## Convenções de Nomenclatura

- **Classes/Objetos**: PascalCase - substantivos (ex: `MinhaClasse`)
- **Atributos**: camelCase - substantivos descritivos (ex: `meuAtributo`)
- **Métodos**: camelCase - verbos ou expressões verbais (ex: `calcularTotal()`)
- Evite abreviações excessivas
- Use nomes descritivos e auto-explicativos
- Mantenha consistência com convenções da linguagem

## Coesão

### Definição

**Coesão** refere-se ao grau de relacionamento entre os membros de uma classe para cumprir uma responsabilidade única e bem definida.

### Características de Classes Coesas

- Responsabilidade única e clara
- Atributos e métodos diretamente relacionados
- Código organizado e legível
- Fácil manutenção e modificação
- Facilita reutilização de código

### Exemplo de Classe Coesa
```java
public class Calculadora {
    public int somar(int a, int b) {
        return a + b;
    }
    
    public int subtrair(int a, int b) {
        return a - b;
    }
    
    public int multiplicar(int a, int b) {
        return a * b;
    }
    
    public double dividir(int a, int b) {
        return (double) a / b;
    }
}
```

### Exemplo de Classe Não Coesa
```java
public class Calculadora {
    // Operações matemáticas (responsabilidade principal)
    public int somar(int a, int b) { ... }
    
    // Funcionalidades não relacionadas
    public void escreverLog(String mensagem) { ... }
    public boolean validarEntradas(int a, int b) { ... }
    public int calcularPotencia(int base, int expoente) { ... }
}
```

**Problema**: Mistura operações básicas com logging, validação e operações avançadas.

## Acoplamento

### Definição

**Acoplamento** descreve o nível de interdependência entre classes. Indica quanto uma classe conhece sobre outras e como se comunicam.

- **Alto acoplamento**: Forte dependência entre classes
- **Baixo acoplamento**: Maior independência entre classes (desejável)

### Problemas do Alto Acoplamento

- Código difícil de compreender e manter
- Alterações geram efeitos colaterais em cascata
- Dificulta testes unitários
- Reduz reutilização de código

### Exemplo de Alto Acoplamento
```java
public class Pedido {
    private Cliente cliente;
    private Estoque estoque;
    private NotificacaoService notificacaoService;
    
    public Pedido(Cliente cliente) {
        this.cliente = cliente;
        this.estoque = new Estoque();  // Dependência direta
        this.notificacaoService = new NotificacaoService();  // Dependência direta
    }
    
    public void adicionarItem(ItemPedido item) {
        if (estoque.verificarDisponibilidade(...)) {
            estoque.atualizarEstoque(...);
            notificacaoService.enviarMensagem(...);
        }
    }
}
```

### Exemplo de Baixo Acoplamento
```java
public class CarrinhoCompras {
    private List<ItemProduto> itens;
    private ServicoEstoque servicoEstoque;
    private ServicoNotificacao servicoNotificacao;
    
    // Injeção de dependência via construtor
    public CarrinhoCompras(ServicoEstoque servicoEstoque, 
                          ServicoNotificacao servicoNotificacao) {
        this.itens = new ArrayList<>();
        this.servicoEstoque = servicoEstoque;
        this.servicoNotificacao = servicoNotificacao;
    }
    
    public void adicionarItem(ItemProduto item) {
        if (servicoEstoque.verificarDisponibilidade(...)) {
            servicoEstoque.atualizarEstoque(...);
            servicoNotificacao.enviarMensagem(...);
            itens.add(item);
        }
    }
}
```

### Práticas para Reduzir Acoplamento

1. **Princípio da Responsabilidade Única**: Cada classe deve ter uma única responsabilidade
2. **Injeção de Dependência**: Fornecer dependências externamente (construtor, métodos, propriedades)
3. **Interfaces e Abstrações**: Depender de abstrações, não de implementações concretas
4. **Design Patterns**: Utilizar padrões como Observer, Strategy
5. **Organização em Camadas**: Separar responsabilidades em módulos distintos
6. **Refatoração Regular**: Revisar código para identificar e reduzir dependências desnecessárias

## Pacotes

### Definição

**Pacotes** são unidades lógicas de agrupamento de classes e elementos relacionados, proporcionando organização e gerenciamento de código.

### Benefícios

- Evita conflitos de nomes (namespaces separados)
- Controla visibilidade de elementos
- Facilita reutilização de código
- Melhora organização e manutenibilidade
- Permite empacotamento em bibliotecas independentes

### Estrutura de Diretórios

Pacotes são representados por diretórios no sistema de arquivos:
```
com/
└── example/
    └── projeto/
        ├── clientes/
        │   └── Cliente.java
        ├── produtos/
        │   └── Produto.java
        └── Main.java
```

### Convenção de Nomenclatura

Formato de domínio reverso: `com.example.projeto`

### Organização de Pacotes

1. **Definir estrutura de diretórios**: Criar hierarquia correspondente aos pacotes
2. **Nomear pacotes**: Usar nomes descritivos em formato de domínio reverso
3. **Organizar classes**: Mover classes para diretórios correspondentes
4. **Gerenciar dependências**: Manter dependências claras e limitadas entre pacotes
5. **Definir visibilidade**: Usar modificadores de acesso apropriados (`public`, `protected`, `private`)
6. **Importar classes**: Usar declaração `import` para acessar classes de outros pacotes

### Exemplo de Declaração
```java
package com.example.projeto.clientes;

import com.example.projeto.produtos.Produto;

public class Cliente {
    // Implementação
}
```

## Modificadores de Acesso

| Modificador | Classe | Pacote | Subclasse | Global |
|-------------|--------|--------|-----------|--------|
| `public` | ✓ | ✓ | ✓ | ✓ |
| `protected` | ✓ | ✓ | ✓ | ✗ |
| (padrão) | ✓ | ✓ | ✗ | ✗ |
| `private` | ✓ | ✗ | ✗ | ✗ |

## Referências

- ARNOLD, K.; GOSLING, J.; HOLMES, D. *The Java Programming Language*. 4th ed. 2005.
- HORSTMANN, C. *Conceitos de Computação com Java*. 5. ed. 2008.
- SCHACH, S. R. *Engenharia de Software*. 7. ed. 2010.
- SCHILDT, H. *Java para Iniciantes*. 6. ed. 2015.

## Ver Também

- [Design Patterns](https://en.wikipedia.org/wiki/Software_design_pattern)
- [SOLID Principles](https://en.wikipedia.org/wiki/SOLID)
- [Java Documentation](https://docs.oracle.com/javase/)