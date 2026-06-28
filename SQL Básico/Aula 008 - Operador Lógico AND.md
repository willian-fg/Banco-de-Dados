# Aula 08 - Operador Lógico AND

## Objetivos

Ao final desta aula você será capaz de:

- Utilizar o operador `AND`.
- Combinar duas ou mais condições.
- Filtrar dados com maior precisão.

---

# O que é o AND?

O operador `AND` significa:

> **E**

Todas as condições devem ser verdadeiras para que o registro seja retornado.

Visualmente:

```text
Condição A = Verdadeira
        E
Condição B = Verdadeira
        ↓
Registro é retornado
```

Se qualquer condição for falsa:

```text
Verdadeiro
    E
Falso
    ↓
Não retorna
```

---

# Sintaxe

```sql
SELECT *
FROM tabela
WHERE condição1
AND condição2;
```

---

# Nossa tabela

| id | nome | idade |
|----|--------|--------|
| 1 | João | 26 |
| 2 | Maria | 35 |
| 3 | Carlos Henrique | 40 |
| 5 | Pedro | 18 |

---

# Exemplo 1

Mostrar clientes com idade maior que 20 **e** menor que 40.

```sql
SELECT *
FROM clientes
WHERE idade > 20
AND idade < 40;
```

Resultado:

| nome | idade |
|-------|--------|
| João | 26 |
| Maria | 35 |

Carlos não aparece porque sua idade é 40.

Pedro não aparece porque tem 18.

---

# Exemplo 2

Mostrar apenas Maria.

```sql
SELECT *
FROM clientes
WHERE nome = 'Maria'
AND idade = 35;
```

Resultado:

| nome | idade |
|-------|--------|
| Maria | 35 |

---

# Exemplo 3

Mostrar João.

```sql
SELECT *
FROM clientes
WHERE id = 1
AND idade = 26;
```

Resultado:

João.

---

# Exemplo 4

Consulta sem resultado.

```sql
SELECT *
FROM clientes
WHERE idade > 50
AND nome = 'João';
```

Resultado:

```text
(0 rows)
```

Não existe nenhum registro que satisfaça ambas as condições.

---

# Fluxo do AND

Imagine:

```text
idade > 20
        │
        E
        │
nome = Maria
        │
        ▼
Resultado
```

As duas precisam ser verdadeiras.

---

# Comparação

Sem AND:

```sql
SELECT *
FROM clientes
WHERE idade > 20;
```

Retorna:

- João
- Maria
- Carlos

---

Com AND:

```sql
SELECT *
FROM clientes
WHERE idade > 20
AND idade < 40;
```

Retorna:

- João
- Maria

---

# Resumo

Nesta aula você aprendeu:

- O operador `AND`.
- Como combinar condições.
- Como restringir consultas.

---

# Exercícios

## Exercício 1

Mostre clientes com idade maior que 25 **e** menor que 40.

---

## Exercício 2

Mostre apenas João utilizando duas condições.

---

## Exercício 3

Mostre clientes com id maior que 1 **e** idade maior que 20.

---

## Exercício 4

Crie uma consulta que não retorne nenhum registro.

---

# Desafio

Crie a tabela:

| produto | preco |
|----------|--------|
| Mouse | 80 |
| Teclado | 180 |
| Webcam | 350 |
| Monitor | 1200 |
| Notebook | 4500 |

Escreva consultas para:

1. Produtos com preço maior que 100 **e** menor que 1000.
2. Produtos com preço maior que 1000 **e** menor que 5000.
3. Produtos chamados "Mouse" **e** com preço igual a 80.

---

# Flashcards

## O que significa AND?

"E".

---

## Quantas condições precisam ser verdadeiras?

Todas.

---

## Quando um registro é retornado?

Quando todas as condições do `AND` forem verdadeiras.

---

# Prática Obrigatória

Execute:

```sql
SELECT *
FROM clientes
WHERE idade > 20
AND idade < 40;
```

Depois:

```sql
SELECT *
FROM clientes
WHERE nome = 'Maria'
AND idade = 35;
```

Depois:

```sql
SELECT *
FROM clientes
WHERE idade > 50
AND nome = 'João';
```

Observe a diferença entre consultas que retornam registros e consultas que retornam `(0 rows)`.
