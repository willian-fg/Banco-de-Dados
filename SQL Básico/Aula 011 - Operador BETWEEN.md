# Aula 11 - Operador BETWEEN

## Objetivos

Ao final desta aula você será capaz de:

- Utilizar o operador `BETWEEN`.
- Filtrar intervalos de valores.
- Trabalhar com números, datas e textos.
- Entender quando utilizar `BETWEEN` em vez de `AND`.

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
- NOT

Nesta aula aprenderemos o operador **BETWEEN**.

---

# O que é BETWEEN?

O operador `BETWEEN` significa:

> **Entre**

Ele verifica se um valor está dentro de um intervalo.

Por exemplo:

```text
Entre 20 e 30
```

Em vez de escrever:

```sql
idade >= 20
AND idade <= 30
```

Podemos escrever:

```sql
idade BETWEEN 20 AND 30
```

Muito mais simples.

---

# Sintaxe

```sql
SELECT *
FROM tabela
WHERE coluna BETWEEN valor_inicial AND valor_final;
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

Mostrar clientes com idade entre 20 e 35.

```sql
SELECT *
FROM clientes
WHERE idade BETWEEN 20 AND 35;
```

Resultado:

| nome | idade |
|-------|--------|
| João | 26 |
| Maria | 35 |

Observe que o 35 foi incluído.

---

# BETWEEN é Inclusivo

Isso significa que os valores inicial e final fazem parte do intervalo.

```sql
BETWEEN 20 AND 35
```

equivale a:

```sql
>= 20
<= 35
```

---

# Comparação

Utilizando AND

```sql
SELECT *
FROM clientes
WHERE idade >= 20
AND idade <= 35;
```

Mesmo resultado.

---

Utilizando BETWEEN

```sql
SELECT *
FROM clientes
WHERE idade BETWEEN 20 AND 35;
```

Mais simples.

---

# Segundo Exemplo

Mostrar clientes com id entre 2 e 5.

```sql
SELECT *
FROM clientes
WHERE id BETWEEN 2 AND 5;
```

Resultado:

Maria

Carlos Henrique

Pedro

---

# Terceiro Exemplo

BETWEEN também funciona com texto.

```sql
SELECT *
FROM clientes
WHERE nome BETWEEN 'Carlos' AND 'Pedro';
```

O PostgreSQL compara os textos em ordem alfabética.

Esse recurso é pouco utilizado, mas existe.

---

# Quarto Exemplo

BETWEEN com datas.

Imagine uma tabela de pedidos.

| id | data |
|----|------------|
|1|2026-07-01|
|2|2026-07-10|
|3|2026-07-20|

Consulta:

```sql
SELECT *
FROM pedidos
WHERE data BETWEEN '2026-07-01' AND '2026-07-15';
```

Resultado:

Pedidos 1 e 2.

---

# NOT BETWEEN

Também podemos negar um intervalo.

```sql
SELECT *
FROM clientes
WHERE idade NOT BETWEEN 20 AND 35;
```

Resultado:

Carlos Henrique

Pedro

---

# Comparação

Sem BETWEEN

```sql
SELECT *
FROM clientes
WHERE idade >= 20
AND idade <= 35;
```

---

Com BETWEEN

```sql
SELECT *
FROM clientes
WHERE idade BETWEEN 20 AND 35;
```

As duas consultas retornam exatamente o mesmo resultado.

---

# Fluxograma

```text
Valor

↓

Está entre os limites?

↓

SIM → Retorna

NÃO → Ignora
```

---

# Resumo

Nesta aula você aprendeu:

- BETWEEN
- NOT BETWEEN
- Intervalos
- Inclusão dos limites
- Uso com números, textos e datas

---

# Exercícios

## Exercício 1

Mostre clientes com idade entre 18 e 30.

---

## Exercício 2

Mostre clientes com id entre 1 e 2.

---

## Exercício 3

Mostre clientes cuja idade NÃO esteja entre 20 e 35.

---

## Exercício 4

Escreva uma consulta utilizando AND e outra utilizando BETWEEN que retornem o mesmo resultado.

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

1. Produtos entre R$100 e R$500.
2. Produtos entre R$1000 e R$5000.
3. Produtos fora do intervalo de R$100 a R$1000.

---

# Flashcards

## O que significa BETWEEN?

Entre.

---

## BETWEEN inclui os limites?

Sim.

---

## BETWEEN substitui qual combinação?

```sql
>=
AND
<=
```

---

## Existe NOT BETWEEN?

Sim.

---

# Prática Obrigatória

Execute:

## Consulta 1

```sql
SELECT *
FROM clientes
WHERE idade BETWEEN 20 AND 35;
```

---

## Consulta 2

```sql
SELECT *
FROM clientes
WHERE id BETWEEN 2 AND 5;
```

---

## Consulta 3

```sql
SELECT *
FROM clientes
WHERE idade NOT BETWEEN 20 AND 35;
```

---

## Consulta 4

Compare estas duas consultas:

```sql
SELECT *
FROM clientes
WHERE idade >= 20
AND idade <= 35;
```

```sql
SELECT *
FROM clientes
WHERE idade BETWEEN 20 AND 35;
```

Verifique que ambas retornam exatamente os mesmos registros.

---

# Curiosidade

O operador `BETWEEN` é muito utilizado em sistemas reais para filtrar:

- Faixas de preço
- Faixas de idade
- Períodos de datas
- Intervalos de códigos
- Relatórios financeiros

Sempre que você precisar consultar um intervalo de valores, considere usar `BETWEEN` para deixar sua consulta mais legível.
