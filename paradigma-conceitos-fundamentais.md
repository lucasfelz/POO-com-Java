# Paradigma de Programação Orientada a Objetos (POO)

## Definição

A **POO** é um paradigma de programação que utiliza **objetos** — estruturas com dados e comportamentos — para abstrair no código as entidades do mundo real.

## Conceitos Fundamentais

### Objetos e Classes

#### Definição de Classe

Uma **classe** é um *blueprint* (projeto/modelo) que define um conjunto de atributos e métodos que os objetos criados a partir dessa classe possuirão.

> **Blueprint** em computação: Espécie de projeto/esboço que funciona como modelo, estrutura ou design detalhado que serve como guia para criação, configuração ou visualização de um sistema, software ou processo. O termo deriva dos blueprints de engenharia civil (projetos arquitetônicos).

#### Definição de Objeto

**Objetos** são instâncias de classes e representam entidades concretas que possuem:
- **Estado**: dados (atributos)
- **Comportamento**: métodos (funcionalidades)

#### Analogia Conceitual: Arquétipos Junguianos

A relação entre interfaces, classes e objetos em POO pode ser compreendida através da psicologia analítica de Jung:

##### Interfaces como Arquétipos

**Interfaces** funcionam como **arquétipos junguianos**:
- São padrões universais de comportamento, sem existência concreta
- Não possuem implementação própria, apenas estrutura (forma pura)
- Representam potencialidades atemporais e não-localizadas
- Definem **o que deve existir**, não **como** se manifesta
- Nunca aparecem "puros" na realidade, sempre através de manifestações concretas
- São contratos que estruturam possibilidades sem materializá-las
```java
// ARQUÉTIPO = INTERFACE (padrão universal)
interface ArquetipoHeroi {
    void enfrentarDesafio();
    void superarObstaculo();
    void retornarTransformado();
}
```

##### Classes como Manifestações Culturais

**Classes** são como **manifestações culturais de arquétipos**:
- Implementações específicas de padrões universais
- Possuem contexto histórico e cultural
- Têm "conteúdo", não apenas "forma"
- Representam formas particulares de concretização do universal
```java
// MANIFESTAÇÃO CULTURAL = CLASSE CONCRETA
class HerculesGrego implements ArquetipoHeroi {
    private String cultura = "Grécia Antiga";
    
    public void enfrentarDesafio() {
        // Os 12 trabalhos de Hércules
    }
    
    public void superarObstaculo() {
        // Usando força física sobrenatural
    }
    
    public void retornarTransformado() {
        // Alcança a imortalidade no Olimpo
    }
}

class LukeSkywalker implements ArquetipoHeroi {
    private String cultura = "Universo Star Wars";
    
    public void enfrentarDesafio() {
        // Destruir a Estrela da Morte
    }
    
    public void superarObstaculo() {
        // Usando a Força
    }
    
    public void retornarTransformado() {
        // Torna-se um Cavaleiro Jedi
    }
}
```

##### Objetos como Experiências Individuais

**Objetos** são **experiências individuais e situadas**:
- Ocorrências únicas no tempo e espaço
- Possuem história e especificidades que a existência traz
- Manifestações concretas de padrões através de formas culturais
```java
// EXPERIÊNCIA INDIVIDUAL = OBJETO (instância concreta)
ArquetipoHeroi jornada1 = new HerculesGrego();
ArquetipoHeroi jornada2 = new LukeSkywalker();

// Mesmo padrão arquetípico, manifestações culturais diferentes
jornada1.retornarTransformado(); // Imortalidade grega
jornada2.retornarTransformado(); // Mestria Jedi
```

##### Hierarquia Ontológica
```
ARQUÉTIPO (Interface)
    ↓ se manifesta como
FORMA CULTURAL (Classe concreta)
    ↓ se concretiza em
EXPERIÊNCIA INDIVIDUAL (Objeto/Instância)
```

| Nível | Conceito Psicológico | Conceito POO | Característica |
|-------|---------------------|--------------|----------------|
| Universal | Arquétipo | Interface | Padrão puro, atemporal |
| Cultural | Manifestação arquetípica | Classe | Forma específica com implementação |
| Individual | Experiência situada | Objeto | Ocorrência única no tempo/espaço |

##### Exemplo Completo: O Arquétipo da Mãe
```java
// ARQUÉTIPO = padrão universal materno
interface ArquetipoMae {
    void nutrir();
    void proteger();
    void transmitirSabedoria();
}

// MANIFESTAÇÃO CULTURAL = forma brasileira contemporânea
class MaeTradicionalBrasileira implements ArquetipoMae {
    private String contexto = "Brasil, século XXI";
    
    public void nutrir() {
        System.out.println("Comida caseira, acolhimento afetivo");
    }
    
    public void proteger() {
        System.out.println("Filho meu não sai de casa sem casaco!");
    }
    
    public void transmitirSabedoria() {
        System.out.println("Ditados populares, histórias de vida");
    }
}

// MANIFESTAÇÃO CULTURAL = forma espartana antiga
class MaeEspartana implements ArquetipoMae {
    private String contexto = "Esparta, Grécia Antiga";
    
    public void nutrir() {
        System.out.println("Treino militar rigoroso desde a infância");
    }
    
    public void proteger() {
        System.out.println("Volte com seu escudo ou sobre ele!");
    }
    
    public void transmitirSabedoria() {
        System.out.println("Valores de coragem, honra e disciplina");
    }
}

// EXPERIÊNCIAS INDIVIDUAIS = pessoas reais
public class Main {
    public static void main(String[] args) {
        // Maria, mãe brasileira específica em 2024
        ArquetipoMae maria = new MaeTradicionalBrasileira();
        maria.nutrir();
        
        // Gorgo, mãe espartana específica em 450 a.C.
        ArquetipoMae gorgo = new MaeEspartana();
        gorgo.proteger();
        
        // Mesmo arquétipo, manifestações culturais diferentes,
        // experiências individuais únicas
    }
}
```

#### Exemplo Prático: Sistema de Biblioteca

**Contexto**: Aplicação de gerenciamento de biblioteca
```java
// Interface (arquétipo do conceito "Livro")
interface ItemBiblioteca {
    void emprestar();
    void devolver();
    String obterInformacoes();
}

// Classe (manifestação específica)
class Livro implements ItemBiblioteca {
    private String titulo;
    private String autor;
    private int anoPublicacao;
    
    public Livro(String titulo, String autor, int anoPublicacao) {
        this.titulo = titulo;
        this.autor = autor;
        this.anoPublicacao = anoPublicacao;
    }
    
    public void emprestar() {
        System.out.println("Livro emprestado");
    }
    
    public void devolver() {
        System.out.println("Livro devolvido");
    }
    
    public String obterInformacoes() {
        return titulo + " - " + autor + " (" + anoPublicacao + ")";
    }
}

// Objeto: instância específica
ItemBiblioteca livro1 = new Livro("20 Mil Léguas Submarinas", "Júlio Verne", 1870);
```

#### Princípio de Identificação

> "Classes são coleções de objetos; portanto, precisamos começar a atividade de programação identificando os objetos e as classes às quais eles pertencem." — Horstmann (2009)

**Refinamento**: Identifique primeiro os **padrões comportamentais** (interfaces/arquétipos), depois as **formas específicas** (classes), e finalmente as **instâncias concretas** (objetos).

### Encapsulamento

#### Definição

**Encapsulamento** é o conceito de manter "escondidos" os detalhes internos de um objeto, fornecendo acesso controlado por meio de métodos públicos.

#### Modificadores de Acesso

| Modificador | Descrição | Visibilidade |
|-------------|-----------|--------------|
| `private` | Acesso restrito à própria classe | Apenas a classe |
| `protected` | Acesso à classe, subclasses e pacote | Classe + herança + pacote |
| `public` | Acesso irrestrito | Global |

#### Benefícios

- **Segurança**: Protege dados contra acesso não autorizado
- **Integridade**: Garante que apenas métodos autorizados modifiquem o estado do objeto
- **Manutenibilidade**: Facilita alterações internas sem impactar código externo

#### Exemplo
```java
class ContaBancaria {
    private double saldo; // Encapsulado
    
    // Acesso controlado
    public double getSaldo() {
        return saldo;
    }
    
    public void depositar(double valor) {
        if (valor > 0) {
            saldo += valor;
        }
    }
}
```

### Herança

#### Definição

**Herança** permite criar novas classes (subclasses) a partir de classes existentes (superclasses). A subclasse herda propriedades e métodos da superclasse, podendo:
- Adicionar novos métodos
- Modificar métodos existentes
- Adicionar novos atributos

#### Terminologia

- **Superclasse**: Classe base/pai
- **Subclasse**: Classe derivada/filha

#### Benefícios

- **Reutilização de código**: Evita duplicação
- **Hierarquia de classes**: Organiza relacionamentos entre entidades
- **Especialização**: Permite criar versões mais específicas de conceitos gerais

#### Exemplo
```java
class Livro {
    protected String titulo;
    protected String autor;
    
    public void emprestar() {
        // implementação base
    }
}

class LivroDigital extends Livro {
    private String formatoArquivo;
    private double tamanhoMB;
    
    public void baixar() {
        // método específico
    }
}

class LivroImpresso extends Livro {
    private int numeroPaginas;
    private String editora;
    
    public void verificarEstadoFisico() {
        // método específico
    }
}
```

**Resultado**: `LivroDigital` e `LivroImpresso` herdam propriedades de `Livro`, mas adicionam características específicas.

### Polimorfismo

#### Definição

**Polimorfismo** permite que objetos de diferentes classes sejam tratados de forma intercambiável se compartilham uma mesma interface ou superclasse.

#### Tipos de Polimorfismo

##### 1. Polimorfismo de Sobrecarga (Overloading)

Permite criar vários métodos com o **mesmo nome**, mas com **diferentes parâmetros**.
```java
class Calculadora {
    // Sobrecarga - mesmo nome, parâmetros diferentes
    public int somar(int a, int b) {
        return a + b;
    }
    
    public double somar(double a, double b) {
        return a + b;
    }
    
    public int somar(int a, int b, int c) {
        return a + b + c;
    }
}
```

##### 2. Polimorfismo de Substituição (Overriding)

Permite que uma subclasse forneça uma **implementação específica** de um método que já existe em sua superclasse.
```java
class Animal {
    public void emitirSom() {
        System.out.println("Som genérico");
    }
}

class Cachorro extends Animal {
    @Override
    public void emitirSom() {
        System.out.println("Au au");
    }
}

class Gato extends Animal {
    @Override
    public void emitirSom() {
        System.out.println("Miau");
    }
}

// Uso polimórfico
Animal animal1 = new Cachorro();
Animal animal2 = new Gato();

animal1.emitirSom(); // "Au au"
animal2.emitirSom(); // "Miau"
```

## Vantagens da POO

### Modularidade
O código é organizado em classes, facilitando:
- Manutenção
- Entendimento
- Separação de responsabilidades

### Reutilização
Classes e objetos podem ser:
- Reutilizados em diferentes partes do programa
- Aproveitados em diferentes projetos
- Estendidos sem modificação

### Extensibilidade
Novas funcionalidades podem ser adicionadas:
- Sem modificar o código existente
- Através de herança
- Mantendo compatibilidade

### Manutenibilidade
A estrutura de classes e objetos facilita:
- Localização de erros
- Correção de bugs
- Evolução do sistema
- Testes isolados

## Resumo dos Pilares da POO

| Pilar | Descrição | Benefício Principal |
|-------|-----------|---------------------|
| **Encapsulamento** | Oculta detalhes internos | Segurança e integridade |
| **Herança** | Reutiliza código de classes existentes | Reaproveitamento |
| **Polimorfismo** | Trata objetos de forma intercambiável | Flexibilidade |
| **Abstração** | Modela conceitos do mundo real | Clareza conceitual |

## Princípios de Design

### Identificação de Interfaces, Classes e Objetos

1. Identifique os **padrões comportamentais** (interfaces/arquétipos)
2. Analise o domínio do problema
3. Identifique as **formas culturais/contextuais** (classes concretas)
4. Defina os atributos (dados) dessas entidades
5. Defina os comportamentos (métodos) dessas entidades
6. Crie a estrutura de interfaces e classes
7. Instancie objetos conforme necessário (experiências individuais)

### Boas Práticas

- Classes devem ter **responsabilidade única** (coesão)
- Minimize **dependências** entre classes (baixo acoplamento)
- **Programe para interfaces, não implementações** (princípio fundamental)
- Favoreça **composição** sobre herança quando apropriado
- Aplique **princípios SOLID**

## Referências

- HORSTMANN, C. *Conceitos de Computação com Java*. 2009.
- JUNG, C. G. *Os Arquétipos e o Inconsciente Coletivo*. Vozes, 2000.

## Ver Também

- [Princípios de Classes em POO](#)
- [SOLID Principles](https://en.wikipedia.org/wiki/SOLID)
- [Design Patterns](https://en.wikipedia.org/wiki/Software_design_pattern)
- [UML - Unified Modeling Language](https://en.wikipedia.org/wiki/Unified_Modeling_Language)
- [Dependency Inversion Principle](https://en.wikipedia.org/wiki/Dependency_inversion_principle)