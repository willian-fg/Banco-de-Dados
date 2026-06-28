# Aula 04 - Consultando Dados com SELECT

## Objetivos

Ao final desta aula você será capaz de:

- Consultar dados de uma tabela.
- Utilizar o comando `SELECT`.
- Selecionar todas as colunas.
- Selecionar colunas específicas.
- Entender a sintaxe básica das consultas.

---

# O que é o SELECT?

Depois de criar uma tabela e inserir registros, precisamos visualizar essas informações.

Para isso utilizamos o comando:

```sql
SELECT
```

O `SELECT` é responsável por consultar dados armazenados em uma tabela.

---

# Nossa Tabela

Imagine a tabela `clientes`.

| id | nome | idade |
|----|-------|--------|
| 1 | João | 25 |
| 2 | Maria | 31 |
| 3 | Carlos | 40 |
| 4 | Ana | 22 |

---

# Sintaxe Básica

```sql
SELECT *
FROM clientes;
```

Resultado:

| id | nome | idade |
|----|-------|--------|
| 1 | João | 25 |
| 2 | Maria | 31 |
| 3 | Carlos | 40 |
| 4 | Ana | 22 |

---

# Entendendo a Sintaxe

```sql
SELECT *
FROM clientes;
```

## SELECT

Informa quais dados queremos consultar.

---

## *

O asterisco (`*`) significa:

> Todas as colunas.

É equivalente a dizer:

```text
id
nome
idade
```

---

## FROM

Significa:

> Da tabela...

---

## clientes

É a tabela onde os dados serão buscados.

---

# Consultando Colunas Específicas

Nem sempre precisamos de todas as informações.

Exemplo:

```sql
SELECT nome
FROM clientes;
```

Resultado:

| nome |
|-------|
| João |
| Maria |
| Carlos |
| Ana |

---

Também podemos consultar mais de uma coluna.

```sql
SELECT nome, idade
FROM clientes;
```

Resultado:

| nome | idade |
|-------|--------|
| João | 25 |
| Maria | 31 |
| Carlos | 40 |
| Ana | 22 |

---

# A Ordem das Colunas

A ordem em que você escreve as colunas será a ordem da saída.

Exemplo:

```sql
SELECT idade, nome
FROM clientes;
```

Resultado:

| idade | nome |
|--------|-------|
| 25 | João |
| 31 | Maria |
| 40 | Carlos |
| 22 | Ana |

---

# Quando usar SELECT *

Utilize `SELECT *` quando:

- estiver estudando;
- quiser conhecer a estrutura da tabela;
- precisar visualizar todos os dados.

Em sistemas reais, prefira selecionar apenas as colunas necessárias.

Bom:

```sql
SELECT nome, idade
FROM clientes;
```

Evite:

```sql
SELECT *
FROM clientes;
```

quando você não precisa de todas as colunas.

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
        │
        ▼
SELECT
```

Agora já conseguimos:

- Criar bancos de dados.
- Criar tabelas.
- Inserir registros.
- Consultar informações.

---

# Resumo

Nesta aula você aprendeu:

- O comando `SELECT`.
- O significado do `*`.
- O comando `FROM`.
- Como selecionar colunas específicas.
- A importância de consultar apenas os dados necessários.

---

# Exercícios

## Exercício 1

Escreva um comando para mostrar todos os dados da tabela `produtos`.

---

## Exercício 2

Mostre apenas a coluna `nome` da tabela `clientes`.

---

## Exercício 3

Mostre apenas:

- nome
- idade

da tabela `clientes`.

---

## Exercício 4

Considere a tabela:

| id | produto | preco | estoque |
|----|----------|--------|----------|
| 1 | Mouse | 80 | 20 |
| 2 | Teclado | 180 | 15 |

Escreva uma consulta que mostre apenas:

- produto
- preco

---

# Desafio

Imagine uma tabela chamada `livros`.

Ela possui:

- id
- titulo
- autor
- ano_publicacao

Escreva:

1. Uma consulta mostrando todas as colunas.
2. Uma consulta mostrando apenas `titulo`.
3. Uma consulta mostrando `titulo` e `autor`.

---

# Flashcards

## Qual comando consulta dados?

```sql
SELECT
```

---

## O que significa `*`?

Selecionar todas as colunas da tabela.

---

## O que faz o `FROM`?

Indica de qual tabela os dados serão consultados.

---

## Como consultar apenas duas colunas?

```sql
SELECT coluna1, coluna2
FROM tabela;
```

---

## É recomendado usar `SELECT *` em sistemas reais?

Não.

Prefira consultar apenas as colunas necessárias.

---