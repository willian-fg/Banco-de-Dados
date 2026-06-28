# Aula 06 - Ordenando Resultados com ORDER BY e LIMIT

## Objetivos

Ao final desta aula você será capaz de:

- Ordenar resultados.
- Ordenar em ordem crescente e decrescente.
- Limitar a quantidade de registros retornados.
- Combinar `SELECT`, `WHERE`, `ORDER BY` e `LIMIT`.

---

# Revisando

Nossa tabela `clientes`:

| id | nome | idade |
|----|-------|--------|
| 1 | João | 25 |
| 2 | Maria | 31 |
| 3 | Carlos | 40 |
| 4 | Ana | 22 |
| 5 | Pedro | 18 |

Até agora sabemos:

- CREATE DATABASE
- CREATE TABLE
- INSERT INTO
- SELECT
- WHERE

Agora veremos como organizar o resultado.

---

# ORDER BY

O comando `ORDER BY` serve para ordenar os registros.

Sintaxe:

```sql
SELECT *
FROM clientes
ORDER BY coluna;
```

---

# Ordem Crescente (ASC)

Por padrão, o PostgreSQL utiliza ordem crescente.

```sql
SELECT *
FROM clientes
ORDER BY idade;
```

Resultado:

| nome | idade |
|-------|--------|
| Pedro | 18 |
| Ana | 22 |
| João | 25 |
| Maria | 31 |
| Carlos | 40 |

Também podemos escrever explicitamente:

```sql
SELECT *
FROM clientes
ORDER BY idade ASC;
```

`ASC` significa:

> Ascending (Crescente)

---

# Ordem Decrescente (DESC)

```sql
SELECT *
FROM clientes
ORDER BY idade DESC;
```

Resultado:

| nome | idade |
|-------|--------|
| Carlos | 40 |
| Maria | 31 |
| João | 25 |
| Ana | 22 |
| Pedro | 18 |

`DESC` significa:

> Descending (Decrescente)

---

# Ordenando por Nome

```sql
SELECT *
FROM clientes
ORDER BY nome;
```

Resultado:

| nome |
|-------|
| Ana |
| Carlos |
| João |
| Maria |
| Pedro |

---

# Ordenando por Mais de uma Coluna

Podemos ordenar utilizando várias colunas.

Exemplo:

```sql
SELECT *
FROM clientes
ORDER BY idade, nome;
```

Primeiro ordena por idade.

Se houver duas pessoas com a mesma idade, organiza pelo nome.

---

# LIMIT

O comando `LIMIT` limita a quantidade de registros retornados.

Sintaxe:

```sql
SELECT *
FROM clientes
LIMIT 3;
```

Resultado:

Retorna apenas os três primeiros registros.

---

# LIMIT com ORDER BY

Essa combinação é muito utilizada.

Mostrar os três clientes mais velhos.

```sql
SELECT *
FROM clientes
ORDER BY idade DESC
LIMIT 3;
```

Resultado:

| nome | idade |
|-------|--------|
| Carlos | 40 |
| Maria | 31 |
| João | 25 |

---

# WHERE + ORDER BY

Podemos combinar comandos.

```sql
SELECT *
FROM clientes
WHERE idade >= 20
ORDER BY idade;
```

Primeiro:

- Filtra.

Depois:

- Ordena.

---

# WHERE + ORDER BY + LIMIT

Também podemos combinar todos.

```sql
SELECT *
FROM clientes
WHERE idade >= 20
ORDER BY idade DESC
LIMIT 2;
```

Fluxo:

1. Filtra.
2. Ordena.
3. Limita.

Resultado:

| nome | idade |
|-------|--------|
| Carlos | 40 |
| Maria | 31 |

---

# Ordem de Execução

Embora escrevamos:

```sql
SELECT
FROM
WHERE
ORDER BY
LIMIT
```

O banco executa aproximadamente nesta ordem:

1. FROM
2. WHERE
3. SELECT
4. ORDER BY
5. LIMIT

Saber isso ajuda a entender consultas mais complexas no futuro.

---

# Resumo

Nesta aula você aprendeu:

- ORDER BY
- ASC
- DESC
- LIMIT
- Como combinar vários comandos.

---

# Exercícios

## Exercício 1

Mostre todos os clientes ordenados pelo nome.

---

## Exercício 2

Mostre todos os clientes do mais velho para o mais novo.

---

## Exercício 3

Mostre apenas os dois primeiros clientes.

---

## Exercício 4

Mostre os três clientes mais novos.

---

## Exercício 5

Mostre os clientes com idade maior que 20, ordenados pelo nome.

---

# Desafio

Considere a tabela:

| produto | preco |
|----------|--------|
| Mouse | 80 |
| Teclado | 180 |
| Monitor | 1200 |
| Notebook | 4500 |
| Webcam | 350 |

Escreva consultas para:

1. Mostrar os produtos do mais barato para o mais caro.
2. Mostrar os dois produtos mais caros.
3. Mostrar os produtos com preço maior que 100, ordenados pelo preço.

---

# Flashcards

## Para que serve o ORDER BY?

Ordenar registros.

---

## O que significa ASC?

Ordem crescente.

---

## O que significa DESC?

Ordem decrescente.

---

## Para que serve LIMIT?

Limitar a quantidade de registros retornados.

---

## Como mostrar os cinco primeiros registros?

```sql
SELECT *
FROM tabela
LIMIT 5;
```

---

## Como mostrar os três maiores salários?

```sql
SELECT *
FROM funcionarios
ORDER BY salario DESC
LIMIT 3;
```

---
