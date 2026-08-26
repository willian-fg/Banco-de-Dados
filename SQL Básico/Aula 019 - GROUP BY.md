# Aula 019 — GROUP BY

## 1. O que é GROUP BY?

O `GROUP BY` é utilizado para **agrupar registros que possuem o mesmo valor** em uma ou mais colunas.

Ele é muito utilizado junto com funções de agregação:

- `COUNT()` → conta registros
- `SUM()` → soma valores
- `AVG()` → calcula média
- `MIN()` → menor valor
- `MAX()` → maior valor

A ideia principal é:

> "Quero pegar vários registros e agrupá-los de acordo com determinada informação."

---

## 2. Exemplo básico

Vamos imaginar esta tabela:

    CREATE TABLE vendas (
        id SERIAL PRIMARY KEY,
        produto VARCHAR(100),
        categoria VARCHAR(50),
        valor DECIMAL(10,2)
    );

Inserindo alguns dados:

    INSERT INTO vendas (produto, categoria, valor)
    VALUES
        ('Notebook', 'Eletrônicos', 3500.00),
        ('Celular', 'Eletrônicos', 2000.00),
        ('Mouse', 'Periféricos', 100.00),
        ('Teclado', 'Periféricos', 200.00),
        ('Monitor', 'Eletrônicos', 1200.00),
        ('Fone', 'Periféricos', 300.00);

A tabela ficará:

| id | produto  | categoria   | valor |
|----|----------|-------------|-------|
| 1  | Notebook | Eletrônicos | 3500  |
| 2  | Celular  | Eletrônicos | 2000  |
| 3  | Mouse    | Periféricos | 100   |
| 4  | Teclado  | Periféricos | 200   |
| 5  | Monitor  | Eletrônicos | 1200  |
| 6  | Fone     | Periféricos | 300   |

---

## 3. GROUP BY sozinho

Podemos fazer:

    SELECT categoria
    FROM vendas
    GROUP BY categoria;

Resultado:

    Eletrônicos
    Periféricos

O PostgreSQL agrupou os registros que possuem a mesma categoria.

---

## 4. GROUP BY + COUNT()

Agora podemos descobrir quantos produtos existem em cada categoria:

    SELECT
        categoria,
        COUNT(*)
    FROM vendas
    GROUP BY categoria;

Resultado:

    categoria      | count
    ---------------+------
    Eletrônicos    | 3
    Periféricos    | 3

Ou seja:

- Eletrônicos → 3 produtos
- Periféricos → 3 produtos

---

## 5. Dando nome ao resultado com AS

Podemos utilizar `AS` para dar um nome mais claro ao resultado:

    SELECT
        categoria,
        COUNT(*) AS quantidade
    FROM vendas
    GROUP BY categoria;

Resultado:

    categoria      | quantidade
    ---------------+-----------
    Eletrônicos    | 3
    Periféricos    | 3

---

## 6. GROUP BY + SUM()

Podemos calcular o valor total de cada categoria:

    SELECT
        categoria,
        SUM(valor) AS total
    FROM vendas
    GROUP BY categoria;

Resultado:

    categoria      | total
    ---------------+-------
    Eletrônicos    | 6700
    Periféricos    | 600

Cálculo:

    Eletrônicos:
    3500 + 2000 + 1200 = 6700

    Periféricos:
    100 + 200 + 300 = 600

---

## 7. GROUP BY + AVG()

Podemos calcular o preço médio dos produtos de cada categoria:

    SELECT
        categoria,
        AVG(valor) AS media
    FROM vendas
    GROUP BY categoria;

Resultado aproximado:

    categoria      | media
    ---------------+---------
    Eletrônicos    | 2233.33
    Periféricos    | 200

---

## 8. GROUP BY + MIN()

Para descobrir o menor valor de cada categoria:

    SELECT
        categoria,
        MIN(valor) AS menor_valor
    FROM vendas
    GROUP BY categoria;

Resultado:

    categoria      | menor_valor
    ---------------+------------
    Eletrônicos    | 1200
    Periféricos    | 100

---

## 9. GROUP BY + MAX()

Para descobrir o maior valor:

    SELECT
        categoria,
        MAX(valor) AS maior_valor
    FROM vendas
    GROUP BY categoria;

Resultado:

    categoria      | maior_valor
    ---------------+------------
    Eletrônicos    | 3500
    Periféricos    | 300

---

## 10. GROUP BY com mais de uma coluna

Também podemos agrupar por mais de uma coluna.

Exemplo:

    SELECT
        categoria,
        produto,
        COUNT(*)
    FROM vendas
    GROUP BY categoria, produto;

Aqui o PostgreSQL considera a combinação:

    categoria + produto

Isso é importante quando trabalhamos com tabelas mais complexas.

---

## 11. GROUP BY + WHERE

Podemos filtrar os registros antes de agrupá-los.

Exemplo:

    SELECT
        categoria,
        COUNT(*) AS quantidade
    FROM vendas
    WHERE valor > 500
    GROUP BY categoria;

A consulta primeiro aplica:

    WHERE valor > 500

Depois realiza:

    GROUP BY categoria

A ordem lógica simplificada é:

    FROM
      ↓
    WHERE
      ↓
    GROUP BY
      ↓
    SELECT
      ↓
    ORDER BY

---

## 12. GROUP BY + ORDER BY

Também podemos ordenar o resultado.

Exemplo:

    SELECT
        categoria,
        SUM(valor) AS total
    FROM vendas
    GROUP BY categoria
    ORDER BY total DESC;

Aqui:

    ORDER BY total DESC

ordena do maior para o menor total.

---

## 13. Uma consulta mais completa

Podemos combinar várias funções:

    SELECT
        categoria,
        COUNT(*) AS quantidade,
        SUM(valor) AS total,
        AVG(valor) AS media,
        MIN(valor) AS menor,
        MAX(valor) AS maior
    FROM vendas
    GROUP BY categoria
    ORDER BY total DESC;

Essa consulta produz um resumo estatístico de cada categoria.

---

## 14. Regra importante do GROUP BY

Quando usamos `GROUP BY`, as colunas que aparecem no `SELECT` precisam, em geral:

1. Estar no `GROUP BY`

OU

2. Estar dentro de uma função de agregação.

Exemplo válido:

    SELECT
        categoria,
        COUNT(*)
    FROM vendas
    GROUP BY categoria;

`categoria` está no `GROUP BY`.

`COUNT(*)` é uma função de agregação.

---

## 15. Exemplo inválido

Esta consulta gera erro:

    SELECT
        categoria,
        produto,
        COUNT(*)
    FROM vendas
    GROUP BY categoria;

Por quê?

Porque `produto` não está no:

    GROUP BY

e também não está dentro de uma função de agregação.

O banco não sabe qual produto deveria representar cada categoria.

---

## 16. Como corrigir?

Uma possibilidade:

    SELECT
        categoria,
        produto,
        COUNT(*)
    FROM vendas
    GROUP BY categoria, produto;

Agora as duas colunas estão no agrupamento.

---

## 17. GROUP BY não é DISTINCT

É importante não confundir:

    SELECT DISTINCT categoria
    FROM vendas;

com:

    SELECT categoria
    FROM vendas
    GROUP BY categoria;

Nesse caso, os resultados podem ser semelhantes.

Porém, a finalidade é diferente.

### DISTINCT

Remove valores duplicados.

    SELECT DISTINCT categoria
    FROM vendas;

### GROUP BY

Agrupa registros para permitir operações sobre cada grupo.

    SELECT
        categoria,
        COUNT(*)
    FROM vendas
    GROUP BY categoria;

Aqui precisamos do `GROUP BY` porque queremos calcular uma quantidade para cada grupo.

---

## 18. Modelo mental

Imagine:

    Eletrônicos
    Eletrônicos
    Eletrônicos
    Periféricos
    Periféricos
    Periféricos

Depois:

    GROUP BY categoria

O banco agrupa conceitualmente:

    Eletrônicos  → Grupo 1
    Periféricos  → Grupo 2

Então podemos realizar operações sobre cada grupo:

    COUNT()
    SUM()
    AVG()
    MIN()
    MAX()

---

## 19. Sintaxe geral

A estrutura mais comum é:

    SELECT
        coluna,
        FUNÇÃO_AGREGADA(coluna)
    FROM tabela
    WHERE condição
    GROUP BY coluna
    ORDER BY coluna;

Exemplo:

    SELECT
        categoria,
        COUNT(*) AS quantidade
    FROM vendas
    WHERE valor > 100
    GROUP BY categoria
    ORDER BY quantidade DESC;

---

# 20. Funções de agregação estudadas

## COUNT()

Conta registros.

    COUNT(*)

---

## SUM()

Soma valores.

    SUM(valor)

---

## AVG()

Calcula a média.

    AVG(valor)

---

## MIN()

Encontra o menor valor.

    MIN(valor)

---

## MAX()

Encontra o maior valor.

    MAX(valor)

---

# 21. Resumo

`GROUP BY`:

> Agrupa registros que possuem valores iguais em determinada coluna.

Exemplo:

    SELECT categoria
    FROM vendas
    GROUP BY categoria;

Com funções de agregação:

    SELECT
        categoria,
        COUNT(*) AS quantidade,
        SUM(valor) AS total,
        AVG(valor) AS media,
        MIN(valor) AS menor,
        MAX(valor) AS maior
    FROM vendas
    GROUP BY categoria;

A ideia fundamental é:

    Tabela
       ↓
    Agrupamento
       ↓
    Função de agregação
       ↓
    Resultado por grupo

---

# 22. Exercício 1

Utilize a tabela:

    vendas (
        id,
        produto,
        categoria,
        valor
    )

Faça uma consulta que mostre:

    categoria | quantidade

A quantidade deve representar quantos produtos existem em cada categoria.

Requisitos:

- Usar `GROUP BY`
- Usar `COUNT()`
- Usar `AS` para nomear a quantidade

Tente fazer sozinho antes de consultar a resposta.

---

# 23. Exercício 2

Mostre o valor total vendido por categoria.

O resultado deve possuir:

    categoria | total

Requisitos:

- Usar `SUM()`
- Usar `GROUP BY`
- Usar `AS`

---

# 24. Exercício 3

Mostre o preço médio dos produtos de cada categoria.

Resultado esperado:

    categoria | media

Requisitos:

- Usar `AVG()`
- Usar `GROUP BY`
- Usar `AS`

---

# 25. Exercício 4

Mostre o maior preço de produto de cada categoria.

Resultado esperado:

    categoria | maior_valor

Requisitos:

- Usar `MAX()`
- Usar `GROUP BY`
- Usar `AS`

---

# 26. Exercício 5

Mostre o menor preço de produto de cada categoria.

Resultado esperado:

    categoria | menor_valor

Requisitos:

- Usar `MIN()`
- Usar `GROUP BY`
- Usar `AS`

---

# 27. Exercício 6 — Desafio

Mostre, para cada categoria:

- quantidade de produtos
- valor total
- valor médio
- menor valor
- maior valor

O resultado deverá possuir aproximadamente:

    categoria | quantidade | total | media | menor_valor | maior_valor

Use:

    COUNT()
    SUM()
    AVG()
    MIN()
    MAX()
    GROUP BY

---

# 28. Próxima aula

Depois de dominar `GROUP BY`, o próximo conceito será:

    HAVING

A diferença fundamental será:

    WHERE  → filtra registros antes do agrupamento

    HAVING → filtra grupos depois do agrupamento

Exemplo que veremos na próxima aula:

    SELECT
        categoria,
        COUNT(*) AS quantidade
    FROM vendas
    GROUP BY categoria
    HAVING COUNT(*) > 2;

Esse conceito é muito importante para consultas SQL mais avançadas.
