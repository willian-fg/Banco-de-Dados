# Aula 02 - Criando seu Primeiro Banco de Dados

## Objetivos

Ao final desta aula você será capaz de:

- Entender o que é SQL.
- Criar um banco de dados.
- Conectar-se a um banco.
- Criar uma tabela.
- Compreender a sintaxe do comando `CREATE TABLE`.

---

# O que é SQL?

**SQL (Structured Query Language)** é a linguagem utilizada para comunicar-se com um banco de dados.

Com SQL podemos:

- Criar bancos de dados.
- Criar tabelas.
- Inserir informações.
- Consultar dados.
- Atualizar registros.
- Remover registros.

Exemplo:

```sql
SELECT * FROM clientes;
```

Esse comando pede ao banco:

> "Mostre todos os registros da tabela clientes."

---

# Criando um Banco de Dados

No PostgreSQL, utilizamos:

```sql
CREATE DATABASE loja;
```

Após executar esse comando, o banco `loja` será criado.

---

# Conectando ao Banco

Depois de criar o banco, precisamos utilizá-lo.

No terminal do PostgreSQL:

```sql
\c loja
```

Saída esperada:

```
You are now connected to database "loja"
```

Agora todos os comandos serão executados dentro desse banco.

---

# Criando uma Tabela

Uma tabela é criada com o comando:

```sql
CREATE TABLE clientes (
    id INTEGER,
    nome VARCHAR(100),
    idade INTEGER
);
```

Agora existe uma tabela chamada `clientes`.

---

# Entendendo a Sintaxe

```sql
CREATE TABLE clientes (
    id INTEGER,
    nome VARCHAR(100),
    idade INTEGER
);
```

Vamos analisar linha por linha.

## CREATE TABLE

Significa:

> Crie uma nova tabela.

---

## clientes

É o nome da tabela.

Poderia ser:

- produtos
- pedidos
- funcionarios
- alunos

---

## id INTEGER

Cria uma coluna chamada `id`.

Tipo:

```text
INTEGER
```

Armazena números inteiros.

Exemplos:

```
1
25
100
999
```

---

## nome VARCHAR(100)

Cria uma coluna chamada `nome`.

Tipo:

```text
VARCHAR(100)
```

Armazena texto de até 100 caracteres.

Exemplo:

```
João
Maria
Carlos
```

---

## idade INTEGER

Outra coluna do tipo inteiro.

---

# Melhorando a Tabela

Na prática quase sempre criamos assim:

```sql
CREATE TABLE clientes (
    id INTEGER PRIMARY KEY,
    nome VARCHAR(100),
    idade INTEGER
);
```

Agora o campo `id` é a chave primária.

Isso significa:

- Não pode repetir.
- Identifica cada cliente.
- Não pode existir dois clientes com o mesmo id.

---

# Convenções de Nomes

Boas práticas:

✅ Use letras minúsculas.

```text
clientes
```

✅ Use underscore para separar palavras.

```text
pedido_item
```

Evite:

```text
Clientes
```

```text
MinhaTabela
```

```text
TabelaClientes
```

---

# Fluxo até agora

```text
CREATE DATABASE
        │
        ▼
Conectar ao Banco
        │
        ▼
CREATE TABLE
        │
        ▼
Tabela pronta
```

---

# Resumo

Nesta aula você aprendeu:

- O que é SQL.
- Como criar um banco.
- Como conectar-se ao banco.
- Como criar tabelas.
- O comando `CREATE TABLE`.
- O conceito de `PRIMARY KEY`.

---

# Exercícios

## Exercício 1

Crie um banco chamado:

```
escola
```

---

## Exercício 2

Crie uma tabela chamada:

```
alunos
```

Com as colunas:

- id
- nome
- idade

Faça o campo `id` ser a chave primária.

---

## Exercício 3

Crie uma tabela chamada:

```
produtos
```

Com as colunas:

- id
- nome
- preco

Escolha o tipo de dado adequado para cada coluna.

---

# Desafio

Crie uma tabela chamada `livros`.

Ela deve possuir:

- id
- titulo
- autor
- ano_publicacao

Escolha os tipos de dados mais adequados.

---

# Flashcards

## O que significa SQL?

Structured Query Language.

---

## Qual comando cria um banco de dados?

```sql
CREATE DATABASE nome;
```

---

## Qual comando cria uma tabela?

```sql
CREATE TABLE nome (...);
```

---

## O que faz o PRIMARY KEY?

Identifica cada registro de forma única.

---

## Qual tipo é usado para armazenar números inteiros?

```text
INTEGER
```

---

## Qual tipo é usado para armazenar textos curtos?

```text
VARCHAR(n)
```

---
