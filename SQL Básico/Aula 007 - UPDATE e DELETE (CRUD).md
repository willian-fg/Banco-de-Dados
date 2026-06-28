# Aula 07 - UPDATE e DELETE (CRUD)

## Objetivos

Ao final desta aula você será capaz de:

- Alterar registros utilizando o comando `UPDATE`.
- Remover registros utilizando o comando `DELETE`.
- Entender a importância do `WHERE`.
- Conhecer boas práticas ao modificar dados.

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

Até agora aprendemos:

- CREATE DATABASE
- CREATE TABLE
- INSERT INTO
- SELECT
- WHERE
- ORDER BY
- LIMIT

Agora veremos como modificar e excluir registros.

---

# UPDATE

O comando `UPDATE` é utilizado para alterar dados existentes.

Sintaxe:

```sql
UPDATE tabela
SET coluna = valor
WHERE condição;
```

---

# Alterando um Registro

Vamos alterar a idade de João para 26.

```sql
UPDATE clientes
SET idade = 26
WHERE id = 1;
```

Agora consultando:

```sql
SELECT *
FROM clientes;
```

Resultado:

| id | nome | idade |
|----|-------|--------|
| 1 | João | 26 |
| 2 | Maria | 31 |
| 3 | Carlos | 40 |
| 4 | Ana | 22 |
| 5 | Pedro | 18 |

---

# Alterando Mais de uma Coluna

```sql
UPDATE clientes
SET
    nome = 'João Silva',
    idade = 27
WHERE id = 1;
```

Resultado:

| id | nome | idade |
|----|------------|--------|
| 1 | João Silva | 27 |

---

# O Perigo de Esquecer o WHERE

Observe este comando:

```sql
UPDATE clientes
SET idade = 18;
```

O que acontece?

👉 Todos os clientes terão idade igual a 18.

Por isso:

> **Nunca execute um UPDATE sem verificar se existe um WHERE**, a menos que sua intenção seja alterar todos os registros.

---

# DELETE

O comando `DELETE` remove registros.

Sintaxe:

```sql
DELETE FROM tabela
WHERE condição;
```

---

# Excluindo um Registro

Excluir Pedro.

```sql
DELETE FROM clientes
WHERE id = 5;
```

Agora:

```sql
SELECT *
FROM clientes;
```

Resultado:

| id | nome | idade |
|----|-------|--------|
| 1 | João Silva | 27 |
| 2 | Maria | 31 |
| 3 | Carlos | 40 |
| 4 | Ana | 22 |

---

# O Perigo do DELETE

Observe:

```sql
DELETE FROM clientes;
```

O que acontece?

👉 Todos os registros da tabela serão removidos.

A tabela continuará existindo, porém ficará vazia.

---

# UPDATE x DELETE

| Comando | Função |
|----------|--------|
| UPDATE | Alterar dados |
| DELETE | Remover registros |

---

# CRUD

CRUD é um acrônimo muito utilizado no desenvolvimento de software.

| Letra | Operação | SQL |
|--------|----------|-----|
| C | Create | INSERT |
| R | Read | SELECT |
| U | Update | UPDATE |
| D | Delete | DELETE |

Todo sistema realiza essas quatro operações.

Exemplos:

- Cadastro de clientes.
- Cadastro de produtos.
- Sistema bancário.
- Redes sociais.
- Aplicativos de delivery.

---

# Resumo

Nesta aula você aprendeu:

- UPDATE.
- DELETE.
- A importância do WHERE.
- O conceito de CRUD.

---

# Exercícios

## Exercício 1

Altere a idade de Maria para 35.

---

## Exercício 2

Altere o nome de Carlos para Carlos Henrique.

---

## Exercício 3

Exclua o cliente Ana.

---

## Exercício 4

Mostre a tabela após cada alteração.

---

# Desafio

Considere a tabela:

| id | produto | preco |
|----|----------|--------|
| 1 | Mouse | 80 |
| 2 | Teclado | 180 |
| 3 | Monitor | 1200 |
| 4 | Notebook | 4500 |

Faça:

1. Altere o preço do Mouse para 90.
2. Altere o nome "Notebook" para "Notebook Gamer".
3. Exclua o Monitor.
4. Liste todos os produtos.

---

# Flashcards

## Para que serve o UPDATE?

Alterar registros.

---

## Para que serve o DELETE?

Remover registros.

---

## O que faz o SET?

Define o novo valor de uma coluna.

---

## Qual a importância do WHERE?

Seleciona quais registros serão alterados ou removidos.

Sem o WHERE, a operação afeta todos os registros.

---

## O que significa CRUD?

- Create
- Read
- Update
- Delete

---

# Prática Obrigatória

Execute no PostgreSQL:

## 1. Verifique os dados

```sql
SELECT * FROM clientes;
```

---

## 2. Atualize João

```sql
UPDATE clientes
SET idade = 26
WHERE id = 1;
```

---

## 3. Confira

```sql
SELECT * FROM clientes;
```

---

## 4. Atualize Maria

```sql
UPDATE clientes
SET idade = 35
WHERE id = 2;
```

---

## 5. Atualize Carlos

```sql
UPDATE clientes
SET nome = 'Carlos Henrique'
WHERE id = 3;
```

---

## 6. Exclua Ana

```sql
DELETE FROM clientes
WHERE id = 4;
```

---

## 7. Veja o resultado final

```sql
SELECT *
FROM clientes;
```

> **Não execute:**

```sql
UPDATE clientes
SET idade = 18;
```

Nem:

```sql
DELETE FROM clientes;
```

Esses comandos modificam ou removem **todos** os registros da tabela.
