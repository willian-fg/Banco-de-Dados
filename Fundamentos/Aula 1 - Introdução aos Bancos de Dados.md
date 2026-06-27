# Aula 01 - Introdução aos Bancos de Dados

## Objetivos

Ao final desta aula você será capaz de:

- Entender o que é um banco de dados.
- Compreender o papel de um SGBD.
- Identificar tabelas, linhas e colunas.
- Entender o conceito de chave primária.
- Conhecer os principais tipos de dados.
- Entender o conceito de relacionamentos.

---

# O que é um Banco de Dados?

Um **Banco de Dados** é uma coleção organizada de informações que podem ser armazenadas, consultadas, modificadas e removidas de forma eficiente.

Imagine o sistema de uma loja.

Ele precisa armazenar:

- Clientes
- Produtos
- Pedidos
- Funcionários

Todas essas informações ficam organizadas em um banco de dados.

Sem um banco de dados, essas informações poderiam estar espalhadas em planilhas ou arquivos de texto, dificultando a organização e a consulta.

---

# O que é um SGBD?

**SGBD** significa **Sistema Gerenciador de Banco de Dados**.

É o software responsável por:

- Armazenar os dados.
- Organizar as informações.
- Controlar o acesso aos dados.
- Executar comandos SQL.
- Garantir a integridade das informações.

Alguns dos SGBDs mais conhecidos:

- PostgreSQL
- MySQL
- SQL Server
- Oracle Database
- SQLite

> **Importante**
>
> SQL **não é** um banco de dados.
>
> SQL é a linguagem utilizada para conversar com um SGBD.

---

# Como um Banco de Dados organiza as informações?

Os dados são organizados em **Tabelas**.

Exemplo:

## Tabela `clientes`

| id | nome | idade |
|----|-------|--------|
| 1 | João | 25 |
| 2 | Maria | 31 |
| 3 | Carlos | 40 |

Essa tabela possui:

- 3 linhas (registros)
- 3 colunas (campos)

---

# Linhas (Registros)

Cada linha representa um registro completo.

Exemplo:

| id | nome | idade |
|----|-------|--------|
| 2 | Maria | 31 |

Essa linha representa apenas uma cliente.

---

# Colunas (Campos)

As colunas representam as características de cada registro.

Na tabela `clientes` temos:

| Coluna | Significado |
|---------|-------------|
| id | Identificador único |
| nome | Nome do cliente |
| idade | Idade |

---

# Chave Primária (Primary Key)

Uma tabela normalmente possui uma coluna responsável por identificar cada registro de forma única.

Essa coluna é chamada de **Chave Primária**.

Exemplo:

| id | nome |
|----|-------|
| 1 | João |
| 2 | Maria |
| 3 | Carlos |

A chave primária:

- Não pode se repetir.
- Normalmente não pode ser nula.
- Identifica exatamente um registro.

---

# Tipos de Dados

Cada coluna possui um tipo de dado.

Alguns dos principais:

| Tipo | Utilização |
|------|------------|
| INTEGER | Números inteiros |
| VARCHAR(100) | Textos curtos |
| TEXT | Textos longos |
| BOOLEAN | Verdadeiro ou falso |
| DATE | Datas |
| DECIMAL | Valores monetários |

Exemplo:

| Coluna | Tipo |
|---------|------|
| id | INTEGER |
| nome | VARCHAR(100) |
| nascimento | DATE |
| salario | DECIMAL(10,2) |

---

# Relacionamentos

Na prática, um banco possui várias tabelas.

## Clientes

| id | nome |
|----|-------|
| 1 | João |
| 2 | Maria |

## Pedidos

| id | cliente_id | valor |
|----|------------|-------|
| 1 | 1 | 150.00 |
| 2 | 1 | 320.00 |
| 3 | 2 | 75.00 |

Observe:

- João possui dois pedidos.
- Maria possui um pedido.

A coluna `cliente_id` conecta um pedido ao cliente.

Esse relacionamento é chamado de **Um para Muitos (1:N)**.

---

# Analogia

Imagine um armário com várias gavetas.

- O armário representa o Banco de Dados.
- Cada gaveta representa uma Tabela.
- Cada ficha dentro da gaveta representa um Registro.
- Cada informação da ficha representa uma Coluna.
- O número da ficha representa a Chave Primária.

---

# Resumo

Nesta aula você aprendeu:

- O que é um Banco de Dados.
- O que é um SGBD.
- O que são Tabelas.
- O que são Linhas.
- O que são Colunas.
- O que é uma Chave Primária.
- Os principais Tipos de Dados.
- O conceito de Relacionamentos.

---

# Exercícios

## Exercício 1

Em uma tabela chamada `alunos`, quais colunas você criaria?

---

## Exercício 2

Qual dessas colunas seria a melhor chave primária?

- nome
- idade
- id
- telefone

Explique sua resposta.

---

## Exercício 3

Escolha o tipo de dado adequado para cada coluna.

| Coluna | Tipo |
|---------|------|
| Nome | |
| Idade | |
| Data de nascimento | |
| Salário | |
| Ativo (Sim/Não) | |

---

# Desafio

Imagine um sistema para uma biblioteca.

Crie:

- Duas tabelas.
- Quatro colunas para cada tabela.

---

# Flashcards

## O que é um Banco de Dados?

Coleção organizada de informações.

---

## O que significa SGBD?

Sistema Gerenciador de Banco de Dados.

---

## O que é uma Tabela?

Estrutura utilizada para armazenar registros.

---

## O que é um Registro?

Uma linha da tabela.

---

## O que é uma Coluna?

Uma característica dos registros.

---

## O que é uma Chave Primária?

Uma coluna que identifica cada registro de forma única.

---

## Cite três SGBDs.

- PostgreSQL
- MySQL
- SQLite

---

## SQL é um Banco de Dados?

Não.

SQL é uma linguagem utilizada para manipular bancos de dados.

---
