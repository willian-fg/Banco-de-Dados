# Aula 15 - NULL, IS NULL e IS NOT NULL

## Objetivos

Ao final desta aula você será capaz de:

- Entender o que é NULL.
- Compreender a diferença entre NULL e outros valores.
- Utilizar IS NULL.
- Utilizar IS NOT NULL.
- Evitar um dos erros mais comuns em SQL.

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
- ILIKE

Hoje aprenderemos um dos conceitos mais importantes da SQL:

**NULL**

---

# O que é NULL?

A maioria dos iniciantes pensa que NULL significa:

> Zero.

Ou:

> Vazio.

Isso está errado.

NULL significa:

> **Valor desconhecido ou inexistente.**

---

# Imagine uma ficha de cadastro

| Nome | Telefone |
|-------|-----------|
| João | 99999-9999 |
| Maria | NULL |

Maria não possui telefone cadastrado.

Isso NÃO significa:

Telefone = ""

Nem:

Telefone = 0

Significa apenas:

> Não sabemos qual é o telefone.

---

# NULL não é um valor

Pense assim.

Imagine uma caixa.

Dentro dela pode existir:

```text
25

"João"

3.14
```

Mas também pode acontecer:

```text
Não sabemos o que existe.
```

Esse "não sabemos" é NULL.

---

# Criando uma tabela

```sql
CREATE TABLE funcionarios (

    id INTEGER PRIMARY KEY,

    nome VARCHAR(100),

    telefone VARCHAR(20)

);
```

---

Inserindo dados.

```sql
INSERT INTO funcionarios
VALUES

(1,'João','99999-9999'),

(2,'Maria',NULL),

(3,'Carlos',NULL),

(4,'Pedro','98888-8888');
```

Tabela.

| id | nome | telefone |
|----|-------|-----------|
|1|João|99999-9999|
|2|Maria|NULL|
|3|Carlos|NULL|
|4|Pedro|98888-8888|

---

# O erro mais comum

Quero encontrar quem não possui telefone.

Muitos iniciantes escrevem:

```sql
SELECT *
FROM funcionarios
WHERE telefone = NULL;
```

Resultado:

```text
0 rows
```

Por quê?

Porque em SQL:

**NULL nunca é igual a nada.**

Nem mesmo a outro NULL.

---

# Como fazer corretamente?

Utilize:

```sql
SELECT *
FROM funcionarios
WHERE telefone IS NULL;
```

Resultado.

Maria

Carlos

---

# IS NULL

Significa:

> O valor é desconhecido?

Sintaxe.

```sql
SELECT *
FROM tabela
WHERE coluna IS NULL;
```

---

# IS NOT NULL

Agora queremos apenas quem possui telefone.

```sql
SELECT *
FROM funcionarios
WHERE telefone IS NOT NULL;
```

Resultado.

João

Pedro

---

# Comparação

Errado.

```sql
telefone = NULL
```

---

Correto.

```sql
telefone IS NULL
```

---

Errado.

```sql
telefone <> NULL
```

---

Correto.

```sql
telefone IS NOT NULL
```

---

# Por que isso acontece?

Imagine uma prova.

Pergunta:

"O João tem telefone?"

Resposta:

```text
Não sabemos.
```

Agora pergunte:

"O telefone do João é igual ao telefone da Maria?"

Resposta:

```text
Não sabemos.
```

Você não pode afirmar igualdade entre duas informações desconhecidas.

É exatamente assim que o SQL trata NULL.

---

# Utilizando AND

```sql
SELECT *
FROM funcionarios
WHERE telefone IS NULL
AND nome LIKE 'M%';
```

Resultado.

Maria

---

# Utilizando OR

```sql
SELECT *
FROM funcionarios
WHERE telefone IS NULL
OR nome = 'Pedro';
```

Resultado.

Maria

Carlos

Pedro

---

# Fluxograma

```text
Campo

↓

Possui valor?

↓

Sim --------→ IS NOT NULL

↓

Não

↓

IS NULL
```

---

# Resumo

Nesta aula você aprendeu:

- NULL
- IS NULL
- IS NOT NULL
- Como evitar o erro mais comum em SQL

---

# Exercícios

## Exercício 1

Mostre todos os funcionários sem telefone.

---

## Exercício 2

Mostre apenas quem possui telefone.

---

## Exercício 3

Mostre funcionários sem telefone cujo nome começa com "C".

---

## Exercício 4

Mostre funcionários que possuem telefone ou cujo nome seja Maria.

---

# Desafio

Crie a tabela:

```text
alunos
```

Campos.

- id
- nome
- email

Cadastre alguns alunos com email e outros sem email.

Depois faça consultas utilizando:

- IS NULL
- IS NOT NULL

---

# Flashcards

## O que significa NULL?

Valor desconhecido ou inexistente.

---

## NULL é igual a zero?

Não.

---

## NULL é uma string vazia?

Não.

---

## Como verificar NULL?

IS NULL.

---

## Como verificar que existe um valor?

IS NOT NULL.

---

## Posso usar "= NULL"?

Não.

---

# Prática Obrigatória

## Consulta 1

```sql
SELECT *
FROM funcionarios
WHERE telefone IS NULL;
```

---

## Consulta 2

```sql
SELECT *
FROM funcionarios
WHERE telefone IS NOT NULL;
```

---

## Consulta 3

```sql
SELECT *
FROM funcionarios
WHERE telefone IS NULL
AND nome LIKE 'M%';
```

---

## Consulta 4

Experimente executar:

```sql
SELECT *
FROM funcionarios
WHERE telefone = NULL;
```

Observe que a consulta não retorna nenhum resultado.

Agora execute:

```sql
SELECT *
FROM funcionarios
WHERE telefone IS NULL;
```

Compare os resultados.

Você verá por que `IS NULL` existe.

---

# Curiosidade

NULL é considerado um dos conceitos que mais causam erros entre iniciantes e até desenvolvedores experientes.

Grande parte dos bugs em consultas SQL acontece porque alguém escreveu:

```sql
= NULL
```

quando deveria ter escrito:

```sql
IS NULL
```

Sempre que precisar verificar se um valor existe ou não existe, lembre-se:

- `IS NULL` → não há valor.
- `IS NOT NULL` → há um valor.
