
# Encapsulamento e Modificadores de Acesso

## Índice

- [Visão Geral](https://claude.ai/chat/d5060d33-e5a2-482a-a0cd-4197deb80b2f#vis%C3%A3o-geral)
- [Níveis de Encapsulamento](https://claude.ai/chat/d5060d33-e5a2-482a-a0cd-4197deb80b2f#n%C3%ADveis-de-encapsulamento)
- [Modificadores de Acesso](https://claude.ai/chat/d5060d33-e5a2-482a-a0cd-4197deb80b2f#modificadores-de-acesso)
    - [public](https://claude.ai/chat/d5060d33-e5a2-482a-a0cd-4197deb80b2f#public)
    - [protected](https://claude.ai/chat/d5060d33-e5a2-482a-a0cd-4197deb80b2f#protected)
    - [default (package-private)](https://claude.ai/chat/d5060d33-e5a2-482a-a0cd-4197deb80b2f#default-package-private)
    - [private](https://claude.ai/chat/d5060d33-e5a2-482a-a0cd-4197deb80b2f#private)
- [Tabela de Visibilidade](https://claude.ai/chat/d5060d33-e5a2-482a-a0cd-4197deb80b2f#tabela-de-visibilidade)
- [Métodos de Acesso (getters e setters)](https://claude.ai/chat/d5060d33-e5a2-482a-a0cd-4197deb80b2f#m%C3%A9todos-de-acesso-getters-e-setters)
- [Exemplos Práticos](https://claude.ai/chat/d5060d33-e5a2-482a-a0cd-4197deb80b2f#exemplos-pr%C3%A1ticos)
    - [Classe Conta](https://claude.ai/chat/d5060d33-e5a2-482a-a0cd-4197deb80b2f#classe-conta)
    - [Classe Aluno](https://claude.ai/chat/d5060d33-e5a2-482a-a0cd-4197deb80b2f#classe-aluno)
    - [Herança e Modificadores](https://claude.ai/chat/d5060d33-e5a2-482a-a0cd-4197deb80b2f#heran%C3%A7a-e-modificadores)
- [Boas Práticas](https://claude.ai/chat/d5060d33-e5a2-482a-a0cd-4197deb80b2f#boas-pr%C3%A1ticas)
- [Referências](https://claude.ai/chat/d5060d33-e5a2-482a-a0cd-4197deb80b2f#refer%C3%AAncias)

---

## Visão Geral

**Encapsulamento** é um dos pilares da Programação Orientada a Objetos (POO). Consiste em elaborar o programa separando suas respectivas partes da forma mais isolada possível, protegendo dados manipulados internamente em uma classe e determinando onde eles podem ser acessados ou modificados.

Benefícios:

- Maior flexibilidade e manutenibilidade do código
- Proteção contra acesso e modificação indevidos
- Redução da complexidade no desenvolvimento
- Facilita novas implementações sem quebrar contratos existentes

> **Nota:** O encapsulamento vincula código e dados de forma segura — é o mecanismo central que garante integridade do estado interno de um objeto.

---

## Níveis de Encapsulamento

O encapsulamento ocorre em dois níveis:

### Nível de Classe

Determina o acesso à classe inteira. Os modificadores possíveis são:

- `public` — acessível de qualquer lugar
- `package-private` (sem modificador) — acessível apenas dentro do mesmo pacote

### Nível de Membro

Determina o acesso a atributos ou métodos individuais da classe. Os modificadores possíveis são:

- `public`
- `protected`
- `default` (package-private)
- `private`

---

## Modificadores de Acesso

### `public`

- Acesso liberado para **qualquer classe**, em qualquer pacote
- Use quando o método ou atributo faz parte da interface pública da classe

```java
public double getSaldo() {
    return saldo;
}
```

### `protected`

- Acesso permitido à **própria classe**, classes do **mesmo pacote** e **subclasses**
- Use quando subclasses precisam acessar ou sobrescrever o comportamento

```java
protected void metodoProtected() {
    System.out.println("animal protected");
}
```

### `default` (package-private)

- Sem nenhuma palavra-chave explícita
- Acesso restrito à **própria classe** e classes do **mesmo pacote**
- Subclasses fora do pacote **não** têm acesso

### `private`

- Acesso restrito **exclusivamente à própria classe**
- Nenhuma outra classe — incluindo subclasses — pode acessar diretamente
- Nível de restrição mais alto; recomendado como padrão para atributos

```java
private double saldo;
```

---

## Tabela de Visibilidade

| Modifier    | Mesma Classe | Mesmo Pacote | Subclasse | Outros (World) |
| ----------- | :----------: | :----------: | :-------: | :------------: |
| `public`    |      ✔       |      ✔       |     ✔     |       ✔        |
| `protected` |      ✔       |      ✔       |     ✔     |       ✘        |
| `default`   |      ✔       |      ✔       |     ✘     |       ✘        |
| `private`   |      ✔       |      ✘       |     ✘     |       ✘        |

---

## Métodos de Acesso (getters e setters)

Como `private` bloqueia qualquer acesso externo — inclusive leitura —, expõe-se o estado interno por meio de métodos públicos controlados:

- **getter** (`get`): retorna o valor de um atributo privado
- **setter** (`set`): define o valor de um atributo privado, podendo incluir validações

```java
// getter
public double getSaldo() {
    return saldo;
}

// setter com validação implícita possível
public void setJuros(double juros) {
    this.juros = juros;
}
```

> **Atenção:** Não exponha setters desnecessariamente. Se um atributo não deve ser alterado externamente, forneça apenas o getter.

---

## Exemplos Práticos

### Classe Conta

Atributos privados com getters/setters e métodos de negócio (`debito`, `credito`):

```java
public class Conta {
    private int    numero;
    private double saldo;
    private double juros;

    // --- getters ---
    public double getJuros()  { return juros;  }
    public int    getNumero() { return numero; }
    public double getSaldo()  { return saldo;  }

    // --- setters ---
    public void setJuros(double juros)   { this.juros  = juros;  }
    public void setNumero(int numero)    { this.numero = numero; }

    // --- métodos de negócio ---
    public void debito(double valor)  { this.saldo -= valor; }
    public void credito(double valor) { this.saldo += valor; }
}
```

O estado de `saldo` só é alterado pelos métodos `debito` e `credito`, garantindo que a conta seja sempre válida.

### Classe Aluno

Inicialização via construtor, leitura via getters sem setters expostos:

```java
class Aluno {
    private String codMatricula;
    private String nome;
    private String cpf;

    Aluno(String tMat, String tNome, String tcpf) {
        codMatricula = tMat;
        nome         = tNome;
        cpf          = tcpf;
    }

    public String codMatricula() { return codMatricula; }
    public String nome()         { return nome;         }
    public String cpf()          { return cpf;          }
}
```

### Herança e Modificadores

```java
class Animal {
    protected void metodoProtected() {
        System.out.println("animal protected");
    }
    private void metodoPrivate() {
        System.out.println("animal private");
    }
}

class Gato extends Animal {
    @Override
    protected void metodoProtected() {        // override válido
        System.out.println("gato protected");
    }
    private void metodoPrivate() {            // método NOVO, não é override
        System.out.println("gato private");
    }
}
```

> **Importante:** `metodoPrivate()` em `Gato` **não** é um override — é um método novo com mesma assinatura. Quando houver referência do tipo `Animal`, será chamado o `metodoPrivate()` de `Animal`.

---

## Boas Práticas

- Declare atributos como `private` por padrão
- Exponha somente o necessário via `public`
- Use `protected` apenas quando a extensão por subclasses for intencional e prevista
- Evite setters desnecessários — prefira inicialização por construtor quando o estado não muda
- Métodos privados podem ser usados internamente para reutilização de lógica sem expô-la

---

## Referências

- NETO, O. M. _Entendendo e dominando o Java_. São Paulo: Digerati, 2004.
- HORSTMANN, C. _Conceitos de computação com o essencial de C++_. 3. ed. Porto Alegre: Bookman, 2005.
- [Encapsulamento, Polimorfismo e Herança em Java — DevMedia](https://www.devmedia.com.br/encapsulamento-polimorfismo-heranca-em-java/12991)
- [Diferença entre modificadores public, default, protected e private — Stack Overflow PT](https://pt.stackoverflow.com/questions/23)