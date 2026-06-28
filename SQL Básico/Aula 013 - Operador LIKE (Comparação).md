# Aula 13 - Operador LIKE

## Objetivos

Ao final desta aula você será capaz de:

- Utilizar o operador `LIKE`.
- Pesquisar textos parcialmente.
- Utilizar os curingas `%` e `_`.
- Compreender quando utilizar `LIKE` em vez de `=`.

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
- >
- <
- >=
- <=
- <>
- BETWEEN
- IN

Hoje aprenderemos o operador **LIKE**.

---

# O que é LIKE?

O operador `LIKE` é utilizado para pesquisar padrões em textos.

Enquanto o operador `=` exige uma correspondência exata:

```sql
WHERE nome = 'João'
```

O `LIKE` permite pesquisas como:

- Começa com...
- Termina com...
- Contém...

---

# Sintaxe

```sql
SELECT *
FROM tabela
WHERE coluna LIKE 'padrão';
```

---

# Nossa tabela

| id | nome | idade |
|----|------------------|--------|
| 1 | João | 26 |
| 2 | Maria | 35 |
| 3 | Carlos Henrique | 40 |
| 4 | José | 31 |
| 5 | Pedro | 18 |

---

# O caractere %

O símbolo `%` significa:

> Zero ou mais caracteres.

Ele funciona como um curinga.

---

# Exemplo 1

Pesquisar nomes que começam com "Jo".

```sql
SELECT *
FROM clientes
WHERE nome LIKE 'Jo%';
```

Resultado:

| nome |
|-------|
| João |
| José |

---

Explicação:

```text
Jo%
```

Significa:

```text
Jo + qualquer sequência de caracteres
```

---

# Exemplo 2

Pesquisar nomes que terminam com "ria".

```sql
SELECT *
FROM clientes
WHERE nome LIKE '%ria';
```

Resultado:

Maria

---

Explicação:

```text
%ria
```

Significa:

```text
qualquer texto + ria
```

---

# Exemplo 3

Pesquisar nomes que contenham "ar".

```sql
SELECT *
FROM clientes
WHERE nome LIKE '%ar%';
```

Resultado:

Maria

Carlos Henrique

---

Explicação:

```text
%ar%
```

Significa:

```text
qualquer texto
+
ar
+
qualquer texto
```

---

# O caractere _

O underline (`_`) representa exatamente **um único caractere**.

---

Exemplo:

```sql
SELECT *
FROM clientes
WHERE nome LIKE 'Jo_o';
```

Resultado:

João

---

Outro exemplo:

```text
A_
```

Aceita:

```text
Ana

Al
```

Mas não:

```text
Amanda
```

Porque há mais de um caractere após o "A".

---

# Comparação

Operador "="

```sql
SELECT *
FROM clientes
WHERE nome = 'João';
```

Resultado:

Apenas João.

---

Operador LIKE

```sql
SELECT *
FROM clientes
WHERE nome LIKE 'Jo%';
```

Resultado:

João

José

---

# LIKE com ORDER BY

```sql
SELECT *
FROM clientes
WHERE nome LIKE 'J%'
ORDER BY nome;
```

Resultado:

João

José

Ordenados alfabeticamente.

---

# LIKE com AND

```sql
SELECT *
FROM clientes
WHERE nome LIKE 'J%'
AND idade > 25;
```

Resultado:

João

José

---

# LIKE com OR

```sql
SELECT *
FROM clientes
WHERE nome LIKE 'J%'
OR idade = 18;
```

Resultado:

João

José

Pedro

---

# Fluxograma

```text
Texto

↓

Corresponde ao padrão?

↓

SIM → Retorna

NÃO → Ignora
```

---

# Resumo

Nesta aula você aprendeu:

- LIKE
- %
- _
- Pesquisa parcial de textos
- Diferença entre "=" e LIKE

---

# Exercícios

## Exercício 1

Mostre clientes cujo nome começa com "C".

---

## Exercício 2

Mostre clientes cujo nome termina com "o".

---

## Exercício 3

Mostre clientes cujo nome contenha "ri".

---

## Exercício 4

Mostre clientes cujo nome começa com "J" e idade maior que 30.

---

# Desafio

Considere a tabela:

| produto |
|----------|
| Mouse Gamer |
| Mouse Sem Fio |
| Teclado Mecânico |
| Webcam HD |
| Notebook Gamer |

Faça consultas para:

1. Produtos que começam com "Mouse".
2. Produtos que terminam com "HD".
3. Produtos que contenham "Gamer".
4. Produtos que começam com "Web".

---

# Flashcards

## Para que serve o LIKE?

Pesquisar padrões em textos.

---

## O que significa %?

Zero ou mais caracteres.

---

## O que significa _?

Exatamente um caractere.

---

## Quando usar LIKE?

Quando a comparação não precisa ser exatamente igual.

---

# Prática Obrigatória

## Consulta 1

```sql
SELECT *
FROM clientes
WHERE nome LIKE 'Jo%';
```

---

## Consulta 2

```sql
SELECT *
FROM clientes
WHERE nome LIKE '%ria';
```

---

## Consulta 3

```sql
SELECT *
FROM clientes
WHERE nome LIKE '%ar%';
```

---

## Consulta 4

```sql
SELECT *
FROM clientes
WHERE nome LIKE 'J%'
ORDER BY nome;
```

---

## Consulta 5

```sql
SELECT *
FROM clientes
WHERE nome LIKE 'J%'
AND idade > 25;
```

---

# Curiosidade

O `LIKE` é muito utilizado em sistemas de busca.

Exemplos:

- Buscar clientes pelo início do nome.
- Pesquisar produtos contendo uma palavra.
- Encontrar cidades que terminam com um determinado sufixo.
- Criar filtros em sistemas ERP, CRM e e-commerce.

Embora seja bastante útil, o `LIKE` diferencia maiúsculas de minúsculas no PostgreSQL. Na próxima aula aprenderemos o operador **ILIKE**, que faz a mesma busca ignorando essa diferença.
