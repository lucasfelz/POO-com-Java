# Princípios de Classes em POO

## Visão Geral

Classes são coleções de objetos e seus nomes devem ser substantivos. Os princípios fundamentais para desenvolvimento de classes são: **coesão**, **acoplamento** e **pacote**.

## Coesão

### Definição

**Coesão** é o princípio da responsabilidade única: uma classe deve assumir apenas uma responsabilidade, sem se apossar daquilo que não é seu dever. Uma boa classe deve representar um único conceito.

### Problema da Falta de Coesão

Quando não respeitado, causa problemas principalmente relacionados à **manutenção** do código.

### Exemplo Incorreto
```java
public class CadastroDeProdutos {
    public void ExibirFormulario() {
        // implementação
    }
    
    public void ObterProduto() {
        // implementação
    }
    
    public void gravarProdutoDB() {
        // implementação
    }
}
```

**Problema**: A classe tem múltiplas responsabilidades (formulário, obtenção e persistência).

### Exemplo Correto
```java
public class Programa {
    public void MostrarFormulario() {
        // implementação
    }
    
    public void BotaoGravarProduto() {
        Produto.gravarProduto();
    }
}
```

**Solução**: A classe responsável pelo cadastro não assume responsabilidades alheias. Seu papel é somente tratar do formulário.

## Acoplamento

### Definição

**Acoplamento** define o grau de dependência entre classes:

- **Alto acoplamento**: Classes muito dependentes umas das outras (fortemente acopladas)
- **Baixo acoplamento**: Classes mais independentes (desejável)

### Problemas do Forte Acoplamento

- Torna difícil compreender as classes isoladamente
- Mudanças em uma classe afetam outras (efeito dominó)
- Difícil de manter
- Difícil de testar
- Difícil de expandir

### Exemplo de Forte Acoplamento
```java
public class X {
    private ClasseConcretaY var1;
    
    void M1(ClasseConcretaW var2) {
        // ...
    }
}
```

**Exemplo prático**:
```java
class Motor {
    void ligar() {
        System.out.println("Motor ligado");
    }
}

class Carro {
    Motor motor = new Motor(); // Dependência direta
    
    void ligarCarro() {
        motor.ligar();
    }
}
```

**Problemas**:
- Mudar `Motor` pode quebrar `Carro`
- Para usar `MotorEletrico`, precisa modificar o código de `Carro`

### Solução: Programar para Interface

> **Princípio fundamental**: Programar para uma interface, não para uma implementação.

A classe deve depender de uma **abstração (interface)** e não de uma classe concreta.

### Exemplo de Baixo Acoplamento
```java
interface IMotor {
    void ligar();
}

class MotorCombustao implements IMotor {
    public void ligar() {
        System.out.println("Motor a combustão ligado");
    }
}

class MotorEletrico implements IMotor {
    public void ligar() {
        System.out.println("Motor elétrico ligado");
    }
}

class Carro {
    IMotor motor; // Depende da interface
    
    Carro(IMotor motor) {
        this.motor = motor;
    }
    
    void ligarCarro() {
        motor.ligar();
    }
}
```

**Uso**:
```java
Carro carro1 = new Carro(new MotorCombustao());
Carro carro2 = new Carro(new MotorEletrico());
```

`Carro` não sabe qual motor está usando, apenas que implementa `IMotor`.

### Comparação

| Forte Acoplamento          | Baixo Acoplamento    |
|----------------------------|----------------------|
| Depende de classe concreta | Depende de interface |
| Difícil de mudar           | Fácil de mudar       |
| Efeito dominó              | Mudanças isoladas    |
| Código rígido              | Código flexível      |

### Benefícios do Baixo Acoplamento

- Código mais flexível
- Mais fácil de testar
- Mais fácil de modificar
- Mais fácil de manter
- Segue princípios SOLID (principalmente DIP - Dependency Inversion Principle)

## Interfaces

### Definição

> **Interface** é um contrato que define quais métodos uma classe deve ter, sem dizer como eles serão implementados.

### Características

- Funciona como um contrato ou lista de regras
- Define **o que** deve existir, não **como** será implementado
- Não é uma classe comum
- Não tem implementação (normalmente)
- Não cria objetos diretamente

### Analogia

Uma interface é como um controle remoto:
- Define botões: ligar(), desligar(), aumentarVolume()
- Não sabe como a TV funciona internamente
- Apenas garante que qualquer TV terá esses métodos

### Exemplo Básico
```java
interface Animal {
    void emitirSom();
}
```

**Significado**: Todo animal precisa ter o método `emitirSom()`.

### Implementação
```java
class Cachorro implements Animal {
    public void emitirSom() {
        System.out.println("Au au");
    }
}

class Gato implements Animal {
    public void emitirSom() {
        System.out.println("Miau");
    }
}
```

**Observação**: Cada classe decide como implementar o comportamento.

### O Que Interface NÃO É
```java
Animal a = new Animal(); // ❌ ERRADO - não se instancia interface
```

Interface é apenas o contrato, não a implementação.

### Vantagens de Programar para Interface

A interface permite trabalhar com tipo genérico, não com algo específico:
```java
Animal animal = new Cachorro();
animal.emitirSom(); // "Au au"

animal = new Gato();
animal.emitirSom(); // "Miau"
```

O código não precisa saber se é cachorro ou gato, apenas que é um `Animal`.

### Benefícios

- Sistema mais flexível
- Mais organizado
- Menos dependente
- Mais fácil de modificar

## Boas Práticas em POO

### Princípios a Aplicar

- **Encapsulamento**
- **Abstração**
- **Herança** (quando bem usada)
- **Polimorfismo**
- **Princípios SOLID**

### Problemas Evitados

- Código frágil
- Código difícil de testar
- Código difícil de manter
- Reescrita desnecessária

### Importância

As boas práticas aplicadas aos projetos orientados a objetos são extremamente importantes para garantir:
- Funcionalidade de classes
- Hierarquia adequada
- Prevenção de problemas que afetariam a entrega e resultado esperado

## Resumo

| Conceito | Descrição | Objetivo |
|----------|-----------|----------|
| **Coesão** | Responsabilidade única por classe | Alta coesão |
| **Acoplamento** | Grau de dependência entre classes | Baixo acoplamento |
| **Interface** | Contrato de métodos sem implementação | Flexibilidade e desacoplamento |

### Regra de Ouro

> Sempre programe para uma interface, não para uma implementação concreta.

## Ver Também

- [SOLID Principles](https://en.wikipedia.org/wiki/SOLID)
- [Dependency Injection](https://en.wikipedia.org/wiki/Dependency_injection)
- [Design by Contract](https://en.wikipedia.org/wiki/Design_by_contract)