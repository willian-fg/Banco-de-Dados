# Aula 05 - Filtrando Dados com WHERE

## Objetivos

Ao final desta aula você será capaz de:

- Filtrar registros utilizando o comando `WHERE`.
- Comparar valores.
- Utilizar operadores relacionais.
- Fazer consultas mais específicas.

---

# Revisando

Nossa tabela `clientes` possui os seguintes dados:

| id | nome | idade |
|----|-------|--------|
| 1 | João | 25 |
| 2 | Maria | 31 |
| 3 | Carlos | 40 |
| 4 | Ana | 22 |
| 5 | Pedro | 18 |

Na aula passada aprendemos:

```sql
SELECT *
FROM clientes;
```

Resultado:

Todos os clientes.

Mas e se quisermos apenas alguns?

É aí que entra o comando:

```sql
WHERE
```

---

# O que é WHERE?

O `WHERE` significa:

> Onde...

Ou seja:

> "Mostre apenas os registros onde determinada condição seja verdadeira."

---

# Sintaxe

```sql
SELECT coluna
FROM tabela
WHERE condição;
```

---

# Igual (=)

Mostrar apenas o cliente de id igual a 3.

```sql
SELECT *
FROM clientes
WHERE id = 3;
```

Resultado:

| id | nome | idade |
|----|-------|--------|
| 3 | Carlos | 40 |

---

# Maior (>)

Mostrar clientes maiores de 30 anos.

```sql
SELECT *
FROM clientes
WHERE idade > 30;
```

Resultado:

| id | nome | idade |
|----|-------|--------|
| 2 | Maria | 31 |
| 3 | Carlos | 40 |

---

# Menor (<)

```sql
SELECT *
FROM clientes
WHERE idade < 25;
```

Resultado:

| id | nome | idade |
|----|-------|--------|
| 4 | Ana | 22 |
| 5 | Pedro | 18 |

---

# Maior ou Igual (>=)

```sql
SELECT *
FROM clientes
WHERE idade >= 25;
```

Resultado:

João, Maria e Carlos.

---

# Menor ou Igual (<=)

```sql
SELECT *
FROM clientes
WHERE idade <= 22;
```

Resultado:

Ana e Pedro.

---

# Diferente (<>)

Também podemos procurar tudo que seja diferente.

```sql
SELECT *
FROM clientes
WHERE idade <> 25;
```

Resultado:

Todos os clientes, exceto João.

---

# Comparando Texto

Também podemos comparar textos.

```sql
SELECT *
FROM clientes
WHERE nome = 'Maria';
```

Resultado:

| id | nome | idade |
|----|-------|--------|
| 2 | Maria | 31 |

Observe:

Textos sempre ficam entre aspas simples.

---

# Operadores Relacionais

| Operador | Significado |
|----------|-------------|
| = | Igual |
| > | Maior |
| < | Menor |
| >= | Maior ou igual |
| <= | Menor ou igual |
| <> | Diferente |

---

# Fluxo

```text
CREATE DATABASE
        │
        ▼
CREATE TABLE
        │
        ▼
INSERT INTO
        │
        ▼
SELECT
        │
        ▼
WHERE
```

Agora conseguimos procurar exatamente o que desejamos.

---

# Resumo

Nesta aula você aprendeu:

- O comando `WHERE`.
- Como comparar números.
- Como comparar textos.
- Os operadores relacionais.
- Como filtrar registros.

---

# Exercícios

## Exercício 1

Mostre apenas o cliente com id igual a 5.

---

## Exercício 2

Mostre todos os clientes com idade maior que 20.

---

## Exercício 3

Mostre todos os clientes com idade menor que 30.

---

## Exercício 4

Mostre apenas o cliente chamado "João".

---

## Exercício 5

Mostre todos os clientes cuja idade seja diferente de 40.

---

# Desafio

Considere a tabela:

| id | produto | preco |
|----|----------|--------|
| 1 | Mouse | 80 |
| 2 | Teclado | 180 |
| 3 | Monitor | 1200 |
| 4 | Notebook | 4500 |

Escreva consultas para:

1. Mostrar apenas produtos com preço maior que 500.
2. Mostrar produtos com preço menor ou igual a 180.
3. Mostrar apenas o produto chamado "Mouse".

---

# Flashcards

## Para que serve o WHERE?

Filtrar registros.

---

## Como procurar um id igual a 10?

```sql
SELECT *
FROM tabela
WHERE id = 10;
```

---

## Como procurar valores maiores que 100?

```sql
WHERE valor > 100;
```

---

## Como procurar valores menores ou iguais a 50?

```sql
WHERE valor <= 50;
```

---

## Como procurar um nome?

```sql
WHERE nome = 'Maria';
```

---

## Como representar "diferente"?

```sql
<>
```

---
