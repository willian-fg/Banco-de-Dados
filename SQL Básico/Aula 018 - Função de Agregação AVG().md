# Aula 18 - Função de Agregação AVG()

## Objetivos

Ao final desta aula você será capaz de:

- Entender o que é a função `AVG()`.
- Calcular médias em colunas numéricas.
- Utilizar `AVG()` com `WHERE`.
- Diferenciar média de soma e contagem.

---

# Revisando

Até agora aprendemos:

## Funções de Agregação

- COUNT() → conta registros
- SUM() → soma valores

Hoje aprenderemos:

- AVG() → calcula média

---

# O que faz AVG()?

A função `AVG()` calcula a **média aritmética** de uma coluna numérica.

Sintaxe:

```sql
SELECT AVG(coluna)
FROM tabela;
```

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

Calcular a média dos preços.

```sql
SELECT AVG(preco)
FROM produtos;
```

### Cálculo manual:

```text
80 + 180 + 350 + 1200 = 1810
1810 / 4 = 452.5
```

Resultado:

```text
452.5
```

---

# Como o PostgreSQL calcula?

Ele faz basicamente:

```text
SUM(coluna) / COUNT(coluna)
```

---

# AVG() ignora NULL

Tabela:

| produto | preco |
|----------|-------|
|Mouse|80|
|Teclado|NULL|
|Webcam|350|
|Monitor|1200|

Consulta:

```sql
SELECT AVG(preco)
FROM produtos;
```

Resultado:

```text
543.33
```

Porque NULL não entra no cálculo.

---

# Comparação com SUM e COUNT

## COUNT

```sql
SELECT COUNT(*)
FROM produtos;
```

Conta linhas.

---

## SUM

```sql
SELECT SUM(preco)
FROM produtos;
```

Soma valores.

---

## AVG

```sql
SELECT AVG(preco)
FROM produtos;
```

Calcula média.

---

# Utilizando WHERE

## Exemplo 1

Média apenas de produtos acima de 100.

```sql
SELECT AVG(preco)
FROM produtos
WHERE preco > 100;
```

Resultado:

```text
576.66
```

---

## Exemplo 2

Média entre 100 e 1000.

```sql
SELECT AVG(preco)
FROM produtos
WHERE preco BETWEEN 100 AND 1000;
```

Resultado:

```text
265
```

---

# Exemplo com Funcionários

| nome | salario |
|------|---------|
|João|2500|
|Maria|3500|
|Carlos|4200|
|Pedro|3000|

Consulta:

```sql
SELECT AVG(salario)
FROM funcionarios;
```

Resultado:

```text
3300
```

---

# Diferença importante

## SUM

```text
Total geral
```

## COUNT

```text
Quantidade de registros
```

## AVG

```text
Valor médio
```

---

# Fluxograma

```text
Tabela

↓

Filtra (WHERE)

↓

Soma valores

↓

Divide pela quantidade

↓

Retorna média
```

---

# Resumo

Nesta aula você aprendeu:

- AVG()
- Média aritmética
- Relação com SUM e COUNT
- Uso com WHERE
- Comportamento com NULL

---

# Exercícios

## Exercício 1

Calcule a média de preços dos produtos.

---

## Exercício 2

Calcule a média apenas dos produtos acima de 300.

---

## Exercício 3

Crie uma tabela de salários e calcule a média.

---

## Exercício 4

Adicione valores NULL e observe como AVG se comporta.

---

# Desafio

Crie a tabela:

| aluno | nota |
|-------|------|
|Ana|8|
|Bruno|7|
|Carlos|NULL|
|Daniel|9|
|Eva|6|

Faça:

1. Média de todas as notas.
2. Média ignorando NULL.
3. Média apenas das notas acima de 7.

---

# Flashcards

## O que faz AVG()?

Calcula a média.

---

## AVG() inclui NULL?

Não.

---

## AVG() é baseado em quê?

SUM / COUNT.

---

## Quando usar AVG()?

Quando quiser calcular médias.

---

# Prática Obrigatória

## Consulta 1

```sql
SELECT AVG(preco)
FROM produtos;
```

---

## Consulta 2

```sql
SELECT AVG(preco)
FROM produtos
WHERE preco > 100;
```

---

## Consulta 3

```sql
SELECT AVG(preco)
FROM produtos
WHERE preco BETWEEN 100 AND 1000;
```

---

## Consulta 4

Compare:

```sql
SELECT SUM(preco) FROM produtos;
```

```sql
SELECT COUNT(preco) FROM produtos;
```

```sql
SELECT AVG(preco) FROM produtos;
```

Entenda a diferença entre total, quantidade e média.

---

# Curiosidade

A função `AVG()` é muito usada em sistemas reais como:

- Média de avaliações de produtos
- Média de notas de alunos
- Média de vendas por dia
- Média salarial por departamento

Sempre que você vê algo como:

```text
Nota média: 4.7 estrelas
```

provavelmente existe um `AVG()` por trás dessa informação.
