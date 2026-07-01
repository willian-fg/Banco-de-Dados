# Aula 16 - Função de Agregação COUNT()

## Objetivos

Ao final desta aula você será capaz de:

- Entender o que é uma função de agregação.
- Utilizar a função `COUNT()`.
- Contar registros de uma tabela.
- Entender a diferença entre `COUNT(*)`, `COUNT(coluna)` e `COUNT(DISTINCT coluna)`.

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

- =
- <>
- >
- <
- >=
- <=
- BETWEEN
- IN
- LIKE
- ILIKE
- IS NULL
- IS NOT NULL

Hoje iniciaremos um novo assunto:

## Funções de Agregação

Nossa primeira função será:

**COUNT()**

---

# O que é uma Função de Agregação?

Até agora nossas consultas retornavam linhas.

Exemplo:

```sql
SELECT *
FROM clientes;
```

Resultado:

| id | nome | idade |
|----|-------|--------|
|1|João|26|
|2|Maria|35|
|3|Carlos|40|
|4|Pedro|18|

Agora queremos obter um resumo.

Exemplo:

> Quantos clientes existem?

Ao invés de receber todas as linhas, receberemos apenas um número.

---

# O que faz COUNT()?

A função `COUNT()` conta registros.

Sintaxe:

```sql
SELECT COUNT(*)
FROM tabela;
```

---

# Primeiro Exemplo

```sql
SELECT COUNT(*)
FROM clientes;
```

Resultado:

| count |
|--------|
| 4 |

Existem quatro registros.

---

# O que significa o *?

No `SELECT` aprendemos que:

```sql
SELECT *
```

significa:

> Todas as colunas.

No `COUNT(*)` o significado é diferente.

Aqui o `*` representa:

> Conte todas as linhas da tabela.

Não importa quantas colunas existam.

---

# COUNT(coluna)

Também podemos contar apenas os valores de uma coluna.

```sql
SELECT COUNT(telefone)
FROM funcionarios;
```

Imagine a tabela:

| nome | telefone |
|-------|-----------|
|João|9999|
|Maria|NULL|
|Carlos|NULL|
|Pedro|8888|

Resultado:

| count |
|--------|
|2|

Por quê?

Porque `COUNT(coluna)` ignora valores NULL.

---

# Diferença

```sql
COUNT(*)
```

Conta todas as linhas.

---

```sql
COUNT(coluna)
```

Conta apenas linhas onde a coluna NÃO é NULL.

---

# Exemplo

Tabela.

| nome | telefone |
|-------|-----------|
|João|9999|
|Maria|NULL|
|Carlos|NULL|
|Pedro|8888|

Consulta:

```sql
SELECT COUNT(*)
FROM funcionarios;
```

Resultado:

```text
4
```

Consulta:

```sql
SELECT COUNT(telefone)
FROM funcionarios;
```

Resultado:

```text
2
```

---

# COUNT(DISTINCT)

Também podemos contar valores únicos.

Tabela.

| cidade |
|---------|
|Campinas|
|São Paulo|
|Campinas|
|Limeira|
|Campinas|

Consulta:

```sql
SELECT COUNT(DISTINCT cidade)
FROM clientes;
```

Resultado:

```text
3
```

Porque existem apenas:

- Campinas
- São Paulo
- Limeira

---

# Utilizando WHERE

Também podemos contar apenas parte da tabela.

```sql
SELECT COUNT(*)
FROM clientes
WHERE idade >= 30;
```

Resultado:

```text
2
```

Maria

Carlos

---

# Utilizando LIKE

```sql
SELECT COUNT(*)
FROM clientes
WHERE nome LIKE 'J%';
```

Resultado:

```text
1
```

---

# Fluxograma

```text
Tabela

↓

Aplica filtros (WHERE)

↓

Conta os registros

↓

Retorna um único número
```

---

# Resumo

Nesta aula você aprendeu:

- O que é uma função de agregação.
- COUNT(*).
- COUNT(coluna).
- COUNT(DISTINCT coluna).
- Como combinar COUNT com WHERE.

---

# Exercícios

## Exercício 1

Conte todos os clientes.

---

## Exercício 2

Conte clientes com idade maior que 30.

---

## Exercício 3

Conte clientes cujo nome começa com "C".

---

## Exercício 4

Crie uma coluna `email` contendo alguns valores NULL e compare:

```sql
COUNT(*)
```

com

```sql
COUNT(email)
```

---

# Desafio

Crie uma tabela chamada produtos.

| produto | categoria |
|----------|-----------|
|Mouse|Periférico|
|Teclado|Periférico|
|Notebook|Computador|
|Monitor|Periférico|
|Servidor|Computador|

Faça:

1. Conte todos os produtos.
2. Conte apenas os periféricos.
3. Conte quantas categorias diferentes existem.

---

# Flashcards

## O que faz COUNT()?

Conta registros.

---

## COUNT(*) conta o quê?

Todas as linhas.

---

## COUNT(coluna) conta o quê?

Somente valores que NÃO são NULL.

---

## COUNT(DISTINCT)?

Conta apenas valores diferentes.

---

# Prática Obrigatória

## Consulta 1

```sql
SELECT COUNT(*)
FROM clientes;
```

---

## Consulta 2

```sql
SELECT COUNT(*)
FROM clientes
WHERE idade >= 30;
```

---

## Consulta 3

```sql
SELECT COUNT(nome)
FROM clientes;
```

---

## Consulta 4

```sql
SELECT COUNT(DISTINCT idade)
FROM clientes;
```

Compare os resultados de cada consulta.

Observe que `COUNT(*)` responde perguntas diferentes de `COUNT(coluna)`.

---

# Curiosidade

O `COUNT()` é uma das funções mais utilizadas em sistemas reais.

Alguns exemplos:

- Quantos usuários estão cadastrados?
- Quantos pedidos foram realizados hoje?
- Quantos produtos existem em estoque?
- Quantos clientes estão ativos?
- Quantos acessos ocorreram neste mês?

Sempre que um sistema exibe um número em um painel ("Total de Clientes", "Pedidos do Dia", "Usuários Online"), existe uma grande chance de que uma consulta com `COUNT()` esteja sendo executada por trás.