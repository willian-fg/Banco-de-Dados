# Aula 17 - Função de Agregação SUM()

## Objetivos

Ao final desta aula você será capaz de:

- Entender o que é a função `SUM()`.
- Somar valores de uma coluna.
- Utilizar `SUM()` com `WHERE`.
- Compreender quando utilizar `SUM()` em aplicações reais.

---

# Revisando

Na aula anterior aprendemos:

```sql
COUNT()
```

Ela responde perguntas como:

- Quantos clientes existem?
- Quantos produtos estão cadastrados?
- Quantos pedidos foram feitos?

Hoje aprenderemos:

```sql
SUM()
```

Ela responde perguntas como:

- Qual o valor total vendido?
- Qual o total em estoque?
- Qual a soma dos salários?

---

# O que faz SUM()?

A função `SUM()` soma os valores de uma coluna numérica.

Sintaxe:

```sql
SELECT SUM(coluna)
FROM tabela;
```

**Importante:**

A coluna deve conter valores numéricos (`INTEGER`, `NUMERIC`, `DECIMAL`, etc.).

---

# Nossa tabela

| id | produto | preco |
|----|----------|-------|
|1|Mouse|80|
|2|Teclado|180|
|3|Webcam|350|
|4|Monitor|1200|

---

# Primeiro Exemplo

Somar todos os preços.

```sql
SELECT SUM(preco)
FROM produtos;
```

Resultado:

```text
1810
```

Cálculo:

```text
80
+180
+350
+1200
------
1810
```

---

# Como o PostgreSQL trabalha?

Imagine a coluna:

```text
80

180

350

1200
```

O PostgreSQL percorre cada linha:

```text
0

↓

80

↓

260

↓

610

↓

1810
```

Depois retorna apenas um valor.

---

# Utilizando WHERE

Somar apenas produtos acima de R$100.

```sql
SELECT SUM(preco)
FROM produtos
WHERE preco > 100;
```

Resultado:

```text
1730
```

Porque:

```text
180

350

1200
```

---

# Outro Exemplo

Tabela.

| funcionário | salario |
|--------------|----------|
|João|2500|
|Maria|3500|
|Carlos|4200|
|Pedro|3000|

Consulta.

```sql
SELECT SUM(salario)
FROM funcionarios;
```

Resultado.

```text
13200
```

---

# SUM() ignora NULL

Tabela.

| nome | salario |
|-------|----------|
|João|2500|
|Maria|NULL|
|Carlos|4200|

Consulta.

```sql
SELECT SUM(salario)
FROM funcionarios;
```

Resultado.

```text
6700
```

O valor NULL não participa da soma.

---

# Comparando

COUNT()

```sql
SELECT COUNT(*)
FROM produtos;
```

Resultado.

```text
4
```

Conta registros.

---

SUM()

```sql
SELECT SUM(preco)
FROM produtos;
```

Resultado.

```text
1810
```

Soma valores.

---

# Utilizando AND

```sql
SELECT SUM(preco)
FROM produtos
WHERE preco > 100
AND preco < 1000;
```

Resultado.

```text
530
```

Porque:

```text
180

350
```

---

# Utilizando BETWEEN

```sql
SELECT SUM(preco)
FROM produtos
WHERE preco BETWEEN 100 AND 1000;
```

Mesmo resultado.

---

# Fluxograma

```text
Tabela

↓

Aplica filtros

↓

Percorre cada linha

↓

Soma os valores

↓

Retorna um único número
```

---

# Resumo

Nesta aula você aprendeu:

- SUM()
- Soma de colunas numéricas
- Uso com WHERE
- Uso com BETWEEN
- Comportamento com NULL

---

# Exercícios

## Exercício 1

Some todos os preços da tabela produtos.

---

## Exercício 2

Some apenas produtos acima de R$300.

---

## Exercício 3

Some apenas produtos entre R$100 e R$500.

---

## Exercício 4

Crie uma coluna chamada estoque.

Some todo o estoque.

---

# Desafio

Crie a tabela:

| Produto | Preço | Estoque |
|----------|--------|----------|
|Mouse|80|30|
|Teclado|180|20|
|Notebook|4500|8|
|Monitor|1200|10|
|Webcam|350|15|

Faça:

1. Soma dos preços.
2. Soma do estoque.
3. Soma dos preços acima de R$500.
4. Soma do estoque apenas dos produtos com preço acima de R$300.

---

# Flashcards

## O que faz SUM()?

Soma valores.

---

## SUM() funciona com texto?

Não.

---

## SUM() funciona com números?

Sim.

---

## SUM() ignora NULL?

Sim.

---

## SUM() pode ser usado com WHERE?

Sim.

---

# Prática Obrigatória

## Consulta 1

```sql
SELECT SUM(preco)
FROM produtos;
```

---

## Consulta 2

```sql
SELECT SUM(preco)
FROM produtos
WHERE preco > 100;
```

---

## Consulta 3

```sql
SELECT SUM(preco)
FROM produtos
WHERE preco BETWEEN 100 AND 1000;
```

---

## Consulta 4

Adicione um produto com preço `NULL`:

```sql
INSERT INTO produtos (produto, preco)
VALUES ('Produto Teste', NULL);
```

Depois execute novamente:

```sql
SELECT SUM(preco)
FROM produtos;
```

Observe que o resultado permanece o mesmo, pois `SUM()` ignora valores `NULL`.

---

# Curiosidade

O `SUM()` é muito utilizado em sistemas de gestão.

Exemplos:

- Total vendido no dia.
- Valor total de um pedido.
- Soma dos salários de um departamento.
- Quantidade total em estoque.
- Receita mensal de uma empresa.

Sempre que você vê um valor como:

```text
Faturamento: R$ 2.350.000
```

há uma boa chance de que esse número tenha sido calculado utilizando `SUM()`.
