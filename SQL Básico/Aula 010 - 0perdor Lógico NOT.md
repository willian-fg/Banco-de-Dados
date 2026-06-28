# Aula 10 - Operador Lógico NOT

## Objetivos

Ao final desta aula você será capaz de:

- Entender o funcionamento do operador `NOT`.
- Negar condições em consultas SQL.
- Combinar `NOT` com outros operadores.
- Escrever consultas mais precisas.

---

# Revisando

Até agora aprendemos:

- CREATE DATABASE
- CREATE TABLE
- INSERT INTO
- SELECT
- WHERE
- ORDER BY
- LIMIT
- UPDATE
- DELETE
- AND
- OR

Nesta aula aprenderemos o operador **NOT**.

---

# O que é NOT?

O operador **NOT** significa:

> **NÃO**

Ele inverte uma condição.

Imagine a condição:

```text
idade = 18
```

Com NOT:

```text
idade NÃO é 18
```

---

# Sintaxe

```sql
SELECT *
FROM tabela
WHERE NOT condição;
```

---

# Nossa tabela

| id | nome | idade |
|----|------------------|--------|
| 1 | João | 26 |
| 2 | Maria | 35 |
| 3 | Carlos Henrique | 40 |
| 5 | Pedro | 18 |

---

# Primeiro Exemplo

Mostrar todos os clientes que NÃO têm 18 anos.

```sql
SELECT *
FROM clientes
WHERE NOT idade = 18;
```

Resultado:

| nome | idade |
|-------|--------|
| João | 26 |
| Maria | 35 |
| Carlos Henrique | 40 |

Pedro não aparece.

---

# Segundo Exemplo

Mostrar todos que NÃO se chamam Maria.

```sql
SELECT *
FROM clientes
WHERE NOT nome = 'Maria';
```

Resultado:

| nome |
|-------|
| João |
| Carlos Henrique |
| Pedro |

---

# Terceiro Exemplo

Mostrar todos que NÃO possuem id igual a 1.

```sql
SELECT *
FROM clientes
WHERE NOT id = 1;
```

Resultado:

Maria

Carlos Henrique

Pedro

---

# NOT com Operadores

Você também pode escrever:

```sql
SELECT *
FROM clientes
WHERE idade <> 18;
```

O resultado será o mesmo de:

```sql
SELECT *
FROM clientes
WHERE NOT idade = 18;
```

As duas consultas são equivalentes.

---

# NOT com AND

```sql
SELECT *
FROM clientes
WHERE NOT (
    idade > 20
    AND idade < 40
);
```

Primeiro o PostgreSQL avalia:

```text
idade > 20
E
idade < 40
```

Depois o NOT inverte o resultado.

---

# NOT com OR

```sql
SELECT *
FROM clientes
WHERE NOT (
    nome = 'João'
    OR nome = 'Maria'
);
```

Resultado:

Carlos Henrique

Pedro

---

# Fluxograma

```text
Condição

↓

Resultado

↓

NOT

↓

Resultado Invertido
```

---

# Comparação

Sem NOT

```sql
SELECT *
FROM clientes
WHERE idade = 18;
```

Resultado:

Pedro

---

Com NOT

```sql
SELECT *
FROM clientes
WHERE NOT idade = 18;
```

Resultado:

João

Maria

Carlos Henrique

---

# Resumo

Nesta aula você aprendeu:

- O operador NOT.
- Como negar condições.
- Como utilizar NOT com AND.
- Como utilizar NOT com OR.

---

# Exercícios

## Exercício 1

Mostre clientes que NÃO possuem idade igual a 35.

---

## Exercício 2

Mostre clientes que NÃO se chamam Pedro.

---

## Exercício 3

Mostre clientes cujo id NÃO seja 3.

---

## Exercício 4

Utilize NOT com AND.

---

# Desafio

Considere a tabela:

| produto | preco |
|----------|--------|
| Mouse | 80 |
| Teclado | 180 |
| Webcam | 350 |
| Monitor | 1200 |
| Notebook | 4500 |

Faça as consultas:

1. Produtos que NÃO custam 80.
2. Produtos que NÃO custam entre 100 e 1000.
3. Produtos que NÃO são "Notebook".

---

# Flashcards

## O que significa NOT?

Negação.

---

## O que o NOT faz?

Inverte o resultado de uma condição.

---

## NOT pode ser usado com AND?

Sim.

---

## NOT pode ser usado com OR?

Sim.

---

# Prática Obrigatória

Execute:

## Consulta 1

```sql
SELECT *
FROM clientes
WHERE NOT idade = 18;
```

---

## Consulta 2

```sql
SELECT *
FROM clientes
WHERE NOT nome = 'Maria';
```

---

## Consulta 3

```sql
SELECT *
FROM clientes
WHERE NOT id = 1;
```

---

## Consulta 4

```sql
SELECT *
FROM clientes
WHERE NOT (
    nome = 'João'
    OR nome = 'Maria'
);
```

Compare os resultados com consultas equivalentes usando `<>` e observe como o `NOT` torna possível negar condições mais complexas.
