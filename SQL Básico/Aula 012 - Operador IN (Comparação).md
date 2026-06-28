# Aula 12 - Operador IN

## Objetivos

Ao final desta aula você será capaz de:

- Utilizar o operador `IN`.
- Substituir vários operadores `OR`.
- Escrever consultas mais limpas.
- Utilizar `NOT IN`.

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

## Operadores Lógicos

- AND
- OR
- NOT

## Operadores de Comparação

- =
- >
- <
- >=
- <=
- <>
- BETWEEN

Hoje aprenderemos o operador **IN**.

---

# O que é IN?

O operador **IN** significa:

> "Está dentro desta lista?"

Ele verifica se um valor pertence a um conjunto de valores.

Imagine a seguinte pergunta:

> O id é 1, 3 ou 5?

Podemos escrever:

```sql
WHERE id = 1
OR id = 3
OR id = 5;
```

Ou simplesmente:

```sql
WHERE id IN (1, 3, 5);
```

Muito mais simples.

---

# Sintaxe

```sql
SELECT *
FROM tabela
WHERE coluna IN (valor1, valor2, valor3);
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

Mostrar clientes de id 1, 3 e 5.

```sql
SELECT *
FROM clientes
WHERE id IN (1, 3, 5);
```

Resultado:

| id | nome |
|----|------------------|
| 1 | João |
| 3 | Carlos Henrique |
| 5 | Pedro |

---

# Comparação

Sem IN

```sql
SELECT *
FROM clientes
WHERE id = 1
OR id = 3
OR id = 5;
```

---

Com IN

```sql
SELECT *
FROM clientes
WHERE id IN (1, 3, 5);
```

Mesmo resultado.

Mais legível.

---

# Segundo Exemplo

Mostrar João e Pedro.

```sql
SELECT *
FROM clientes
WHERE nome IN ('João', 'Pedro');
```

Resultado:

| nome |
|-------|
| João |
| Pedro |

---

# Terceiro Exemplo

Mostrar clientes com idade 18, 26 ou 40.

```sql
SELECT *
FROM clientes
WHERE idade IN (18, 26, 40);
```

Resultado:

Pedro

João

Carlos Henrique

---

# NOT IN

Também podemos negar a lista.

```sql
SELECT *
FROM clientes
WHERE id NOT IN (1, 3);
```

Resultado:

Maria

Pedro

---

# IN com ORDER BY

```sql
SELECT *
FROM clientes
WHERE idade IN (18, 26, 40)
ORDER BY idade;
```

Resultado:

Pedro

João

Carlos Henrique

Ordenados pela idade.

---

# Fluxograma

```text
Valor

↓

Está dentro da lista?

↓

SIM → Retorna

NÃO → Ignora
```

---

# Comparação

OR

```sql
WHERE nome = 'João'
OR nome = 'Pedro'
OR nome = 'Maria'
```

IN

```sql
WHERE nome IN (
    'João',
    'Pedro',
    'Maria'
)
```

Sempre prefira `IN` quando estiver comparando a mesma coluna com vários valores.

---

# Resumo

Nesta aula você aprendeu:

- IN
- NOT IN
- Comparação com OR
- Consultas utilizando listas

---

# Exercícios

## Exercício 1

Mostre clientes de id 2 e 5.

---

## Exercício 2

Mostre João e Maria utilizando IN.

---

## Exercício 3

Mostre clientes com idade 18 ou 35.

---

## Exercício 4

Mostre clientes cujo id NÃO esteja em (2, 3).

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

Escreva consultas para:

1. Mostrar Mouse, Webcam e Notebook.
2. Mostrar produtos com preço 80, 350 e 1200.
3. Mostrar produtos que NÃO sejam Mouse nem Monitor.

---

# Flashcards

## O que significa IN?

Pertence à lista.

---

## IN substitui qual operador?

OR.

---

## Existe NOT IN?

Sim.

---

## Quando usar IN?

Quando uma coluna precisa ser comparada com vários valores.

---

# Prática Obrigatória

## Consulta 1

```sql
SELECT *
FROM clientes
WHERE id IN (1, 3, 5);
```

---

## Consulta 2

```sql
SELECT *
FROM clientes
WHERE nome IN ('João', 'Pedro');
```

---

## Consulta 3

```sql
SELECT *
FROM clientes
WHERE idade IN (18, 26, 40);
```

---

## Consulta 4

```sql
SELECT *
FROM clientes
WHERE id NOT IN (1, 3);
```

---

## Consulta 5

Compare estas duas consultas:

```sql
SELECT *
FROM clientes
WHERE id = 1
OR id = 3
OR id = 5;
```

```sql
SELECT *
FROM clientes
WHERE id IN (1, 3, 5);
```

Observe que ambas retornam exatamente o mesmo resultado.

A diferença é que `IN` torna o código mais limpo, legível e fácil de manter.

---

# Curiosidade

O operador `IN` é muito utilizado em sistemas reais quando recebemos uma lista de valores.

Exemplo:

Um usuário seleciona vários produtos para pesquisar.

A aplicação pode gerar uma consulta como:

```sql
SELECT *
FROM produtos
WHERE id IN (3, 7, 15, 22, 40);
```

Esse padrão aparece com frequência em APIs, sistemas de gestão, e-commerce e relatórios.
