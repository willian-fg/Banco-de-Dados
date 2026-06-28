# PostgreSQL - Guia Rápido

> Sistema Operacional: Linux Lite (Ubuntu/Debian)

---

# Iniciar o serviço PostgreSQL

Verificar se o serviço está ativo.

```bash
sudo systemctl status postgresql
```

Caso não esteja iniciado:

```bash
sudo systemctl start postgresql
```

Iniciar automaticamente junto com o sistema:

```bash
sudo systemctl enable postgresql
```

---

# Entrar no PostgreSQL

Entrar como administrador:

```bash
sudo -u postgres psql
```

Ou utilizando um usuário criado por você:

```bash
psql -U will -d loja
```

---

# Comandos do psql

Listar bancos:

```sql
\l
```

Conectar em um banco:

```sql
\c loja
```

Listar tabelas:

```sql
\dt
```

Descrever uma tabela:

```sql
\d clientes
```

Limpar a tela:

```sql
\! clear
```

Sair do PostgreSQL:

```sql
\q
```

---

# Criar um Banco de Dados

```sql
CREATE DATABASE loja;
```

Conectar ao banco:

```sql
\c loja
```

---

# Criar uma Tabela

```sCEateprodutosql
CREATE TABLE clientes (
    id INTEGER PRIMARY KEY,
    nome VARCHAR(100),
    idade INTEGER
);
```

---

# Inserir um Registro

```sql
INSERT INTO clientes
VALUES (1, 'João', 25);
```

---

# Inserir Vários Registros

```sql
INSERT INTO clientes
VALUES
(2, 'Maria', 31),
(3, 'Carlos', 40),
(4, 'Ana', 22),
(5, 'Pedro', 18);
```

---

# Consultar Todos os Dados

```sql
SELECT *
FROM clientes;
```

---

# Consultar Apenas uma Coluna

```sql
SELECT nome
FROM clientes;
```

---

# Consultar Mais de uma Coluna

```sql
SELECT nome, idade
FROM clientes;
```

---

# Filtrar Dados

Igual:

```sql
SELECT *
FROM clientes
WHERE id = 1;
```

Maior:

```sql
SELECT *
FROM clientes
WHERE idade > 30;
```

Menor:

```sql
SELECT *
FROM clientes
WHERE idade < 25;
```

Maior ou igual:

```sql
SELECT *
FROM clientes
WHERE idade >= 25;
```

Menor ou igual:

```sql
SELECT *
FROM clientes
WHERE idade <= 22;
```

Diferente:

```sql
SELECT *
FROM clientes
WHERE idade <> 25;
```

Texto:

```sql
SELECT *
FROM clientes
WHERE nome = 'Maria';
```

---

# Ordenação

Crescente:

```sql
SELECT *
FROM clientes
ORDER BY idade ASC;
```

Decrescente:

```sql
SELECT *
FROM clientes
ORDER BY idade DESC;
```

Por nome:

```sql
SELECT *
FROM clientes
ORDER BY nome;
```

---

# LIMIT

```sql
SELECT *
FROM clientes
LIMIT 3;
```

---

# Consulta Completa

```sql
SELECT nome, idade
FROM clientes
WHERE idade >= 20
ORDER BY idade DESC
LIMIT 2;
```

---

# Operadores

| Operador | Significado |
|-----------|-------------|
| = | Igual |
| > | Maior |
| < | Menor |
| >= | Maior ou igual |
| <= | Menor ou igual |
| <> | Diferente |

---

# Tipos de Dados

| Tipo | Utilização |
|-------|------------|
| INTEGER | Inteiros |
| VARCHAR(100) | Texto curto |
| TEXT | Texto longo |
| BOOLEAN | Verdadeiro/Falso |
| DATE | Datas |
| DECIMAL(10,2) | Valores monetários |

---

# Ordem de uma Consulta

```sql
SELECT colunas
FROM tabela
WHERE condição
ORDER BY coluna ASC | DESC
LIMIT quantidade;
```

---

# Fluxo de Trabalho

```text
Abrir Terminal
      │
      ▼
Iniciar PostgreSQL
      │
      ▼
Entrar no psql
      │
      ▼
Conectar ao Banco
      │
      ▼
Criar Tabelas
      │
      ▼
Inserir Dados
      │
      ▼
Consultar Dados
      │
      ▼
Sair (\q)
```

---

# Encerrar Sessão

Dentro do PostgreSQL:

```sql
\q
```

No terminal, o PostgreSQL continuará em execução como um serviço. Normalmente **não é necessário pará-lo**.

Se, por algum motivo, você quiser parar o serviço:

```bash
sudo systemctl stop postgresql
```
