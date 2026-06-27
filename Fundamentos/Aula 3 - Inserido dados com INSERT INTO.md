# Aula 03 - Inserindo Dados com INSERT INTO

## Objetivos

Ao final desta aula você será capaz de:

- Inserir registros em uma tabela.
- Entender a sintaxe do comando `INSERT INTO`.
- Inserir um ou vários registros de uma vez.
- Conhecer boas práticas ao inserir dados.

---

# O que é o INSERT INTO?

Depois de criar uma tabela, ela está vazia.

Exemplo:

## Tabela `clientes`

| id | nome | idade |
|----|------|--------|
|    |      |        |

Para adicionar registros utilizamos o comando:

```sql
INSERT INTO
```

---

# Sintaxe Básica

```sql
INSERT INTO nome_da_tabela
VALUES (...);
```

Exemplo:

```sql
INSERT INTO clientes
VALUES (1, 'João', 25);
```

Agora a tabela possui:

| id | nome | idade |
|----|------|--------|
| 1 | João | 25 |

---

# Entendendo a Sintaxe

```sql
INSERT INTO clientes
VALUES (1, 'João', 25);
```

## INSERT INTO

Significa:

> Inserir dados em uma tabela.

---

## clientes

É o nome da tabela.

---

## VALUES

Indica os valores que serão inseridos.

---

## (1, 'João', 25)

Os valores devem seguir exatamente a ordem das colunas.

Tabela:

| id | nome | idade |
|----|------|--------|

Valores:

```
id    → 1
nome  → João
idade → 25
```

---

# Inserindo Outro Registro

```sql
INSERT INTO clientes
VALUES (2, 'Maria', 31);
```

Tabela:

| id | nome | idade |
|----|------|--------|
| 1 | João | 25 |
| 2 | Maria | 31 |

---

# Inserindo Vários Registros

Também podemos inserir vários registros em um único comando.

```sql
INSERT INTO clientes
VALUES
(3, 'Carlos', 40),
(4, 'Ana', 22),
(5, 'Pedro', 29);
```

Resultado:

| id | nome | idade |
|----|------|--------|
| 1 | João | 25 |
| 2 | Maria | 31 |
| 3 | Carlos | 40 |
| 4 | Ana | 22 |
| 5 | Pedro | 29 |

Essa forma é mais eficiente do que executar vários comandos separados.

---

# Informando as Colunas

Também podemos indicar explicitamente quais colunas receberão valores.

```sql
INSERT INTO clientes (id, nome, idade)
VALUES (6, 'Lucas', 19);
```

Isso torna o código mais legível e evita erros caso a estrutura da tabela seja alterada.

---

# Inserindo Apenas Algumas Colunas

Suponha a tabela:

| id | nome | idade | telefone |
|----|------|--------|-----------|

Podemos fazer:

```sql
INSERT INTO clientes (id, nome)
VALUES (7, 'Fernanda');
```

As colunas não informadas receberão o valor padrão (`NULL`), caso permitido.

---

# Cuidados

### Texto

Textos devem ficar entre aspas simples.

Correto:

```sql
'Maria'
```

Errado:

```sql
Maria
```

---

### Números

Números não usam aspas.

Correto:

```sql
25
```

Errado:

```sql
'25'
```

---

# Fluxo até agora

```text
CREATE DATABASE
        │
        ▼
CREATE TABLE
        │
        ▼
INSERT INTO
```

Agora já sabemos:

- criar bancos;
- criar tabelas;
- inserir registros.

---

# Resumo

Nesta aula você aprendeu:

- O comando `INSERT INTO`.
- Como inserir um registro.
- Como inserir vários registros.
- Como informar as colunas.
- A importância da ordem dos valores.

---

# Exercícios

## Exercício 1

Considere a tabela:

```text
alunos
---------
id
nome
idade
```

Insira os seguintes alunos:

- João - 18 anos
- Maria - 20 anos
- Pedro - 17 anos

---

## Exercício 2

Crie um comando que insira três produtos:

- Mouse
- Teclado
- Monitor

Escolha um preço para cada um.

---

## Exercício 3

Escreva um comando utilizando:

```sql
INSERT INTO tabela (colunas...)
```

---

# Desafio

Imagine uma tabela chamada `livros`.

Ela possui:

- id
- titulo
- autor
- ano_publicacao

Insira cinco livros diferentes.

---

# Flashcards

## Qual comando insere dados?

```sql
INSERT INTO
```

---

## O que faz o VALUES?

Informa os valores que serão inseridos.

---

## Os valores precisam seguir qual ordem?

A mesma ordem das colunas da tabela.

---

## Como inserir vários registros?

Separando cada conjunto de valores por vírgulas.

---

## Como representar textos?

Entre aspas simples.

Exemplo:

```sql
'João'
```

---

## Como representar números?

Sem aspas.

Exemplo:

```sql
25
```