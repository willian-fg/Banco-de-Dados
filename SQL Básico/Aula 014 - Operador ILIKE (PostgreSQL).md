# Aula 14 - Operador ILIKE (PostgreSQL)

## Objetivos

Ao final desta aula você será capaz de:

- Entender o funcionamento do operador `ILIKE`.
- Compreender a diferença entre `LIKE` e `ILIKE`.
- Realizar pesquisas ignorando letras maiúsculas e minúsculas.
- Saber quando utilizar cada operador.

---

# Revisando

Até agora aprendemos:

## DDL

- CREATE DATABASE
- CREATE TABLE

## DML

- INSERT
- UPDATE
- DELETE

## DQL

- SELECT
- WHERE
- ORDER BY
- LIMIT

## Operadores Lógicos

- AND
- OR
- NOT

## Operadores de Comparação

### Comparação Simples

- =
- <>
- >
- <
- >=
- <=

### Comparação por Intervalo

- BETWEEN

### Comparação por Lista

- IN

### Comparação por Padrão

- LIKE

Hoje aprenderemos:

**ILIKE**

---

# O que é ILIKE?

O operador `ILIKE` funciona exatamente como o `LIKE`, porém:

> **Ignora letras maiúsculas e minúsculas.**

---

# IMPORTANTE

`ILIKE` **não faz parte do padrão SQL**.

Ele é uma funcionalidade do PostgreSQL.

Se você trocar de banco (MySQL, SQL Server, Oracle...), talvez ele não exista.

---

# Nossa tabela

| id | nome | idade |
|----|------------------|--------|
| 1 | João | 26 |
| 2 | MARIA | 35 |
| 3 | Carlos Henrique | 40 |
| 4 | josé | 31 |
| 5 | PEDRO | 18 |

Observe que agora existem nomes escritos de formas diferentes.

---

# Problema com LIKE

Consulta:

```sql
SELECT *
FROM clientes
WHERE nome LIKE 'jo%';
```

Resultado:

Nenhum registro.

Por quê?

Porque:

```text
João

≠

joão
```

O PostgreSQL diferencia maiúsculas de minúsculas.

---

# Utilizando ILIKE

```sql
SELECT *
FROM clientes
WHERE nome ILIKE 'jo%';
```

Resultado:

João

josé

Agora a pesquisa funciona.

---

# Outro Exemplo

```sql
SELECT *
FROM clientes
WHERE nome ILIKE '%ria';
```

Resultado:

MARIA

Mesmo estando em letras maiúsculas.

---

# Mais um Exemplo

```sql
SELECT *
FROM clientes
WHERE nome ILIKE '%RO%';
```

Resultado:

PEDRO

Carlos Henrique

O PostgreSQL ignora a diferença entre maiúsculas e minúsculas.

---

# Comparação

LIKE

```sql
WHERE nome LIKE 'jo%'
```

Resultado:

Depende das letras estarem exatamente iguais.

---

ILIKE

```sql
WHERE nome ILIKE 'jo%'
```

Resultado:

Ignora letras maiúsculas e minúsculas.

---

# LIKE x ILIKE

| Operador | Maiúsculas importam? |
|-----------|----------------------|
| LIKE | Sim |
| ILIKE | Não |

---

# Quando usar LIKE?

Quando a diferença entre letras maiúsculas e minúsculas for importante.

Exemplo:

Senhas.

Códigos.

Identificadores.

---

# Quando usar ILIKE?

Na maioria das pesquisas realizadas por usuários.

Exemplo:

Pesquisar clientes.

Pesquisar produtos.

Pesquisar cidades.

Pesquisar livros.

Pesquisar músicas.

---

# Utilizando ORDER BY

```sql
SELECT *
FROM clientes
WHERE nome ILIKE '%a%'
ORDER BY nome;
```

---

# Utilizando AND

```sql
SELECT *
FROM clientes
WHERE nome ILIKE 'j%'
AND idade > 25;
```

---

# Utilizando OR

```sql
SELECT *
FROM clientes
WHERE nome ILIKE 'm%'
OR idade = 18;
```

---

# Resumo

Nesta aula você aprendeu:

- ILIKE
- Diferença entre LIKE e ILIKE
- Pesquisa sem diferenciar maiúsculas e minúsculas

---

# Exercícios

## Exercício 1

Mostre nomes iniciados por "c".

---

## Exercício 2

Mostre nomes terminados em "o".

---

## Exercício 3

Mostre nomes contendo "ri".

---

## Exercício 4

Utilize ILIKE juntamente com AND.

---

# Desafio

Crie uma tabela chamada produtos.

Insira:

| Produto |
|----------|
| Mouse Gamer |
| mouse sem fio |
| Teclado Mecânico |
| NOTEBOOK |
| Webcam HD |

Agora faça:

1. Pesquise produtos iniciados por "mouse".
2. Pesquise produtos contendo "gamer".
3. Pesquise produtos terminados em "hd".

Utilize apenas ILIKE.

---

# Flashcards

## O que faz o ILIKE?

Pesquisa padrões ignorando letras maiúsculas e minúsculas.

---

## ILIKE faz parte do SQL padrão?

Não.

É um recurso do PostgreSQL.

---

## Quando usar ILIKE?

Quando a pesquisa for realizada por usuários.

---

## Diferença entre LIKE e ILIKE?

LIKE diferencia maiúsculas de minúsculas.

ILIKE ignora essa diferença.

---

# Prática Obrigatória

## Consulta 1

```sql
SELECT *
FROM clientes
WHERE nome ILIKE 'jo%';
```

---

## Consulta 2

```sql
SELECT *
FROM clientes
WHERE nome ILIKE '%ria';
```

---

## Consulta 3

```sql
SELECT *
FROM clientes
WHERE nome ILIKE '%ro%';
```

---

## Consulta 4

```sql
SELECT *
FROM clientes
WHERE nome ILIKE 'j%'
AND idade > 25;
```

Compare os resultados obtidos com os mesmos comandos utilizando `LIKE`.

Observe como `ILIKE` torna as pesquisas mais amigáveis para o usuário.

---

# Curiosidade

Em aplicações web desenvolvidas com Python e PostgreSQL (como FastAPI + SQLAlchemy), é muito comum utilizar `ILIKE` para implementar o campo de pesquisa.

Exemplo:

O usuário digita:

```text
jo
```

E o sistema encontra:

- João
- josé
- JOANA

Mesmo que a capitalização seja diferente.
