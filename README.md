# Pesquisa sobre Bibliotecas Python para Conexão com Bancos de Dados

## Disciplina

Tópicos Avançados de Programação

## Integrantes

* Diogo Jacob
* Felipe Machado
* Jhon Alison
* Victor Hugo

## Objetivo

Este trabalho tem como objetivo pesquisar e comparar bibliotecas da linguagem Python utilizadas para realizar a conexão entre aplicações e bancos de dados.

Serão analisadas diferentes bibliotecas, observando suas principais características, os bancos de dados suportados, a forma de instalação e a maneira como são realizadas conexões e consultas.

As bibliotecas pesquisadas serão:

* pyodbc
* pymssql
* psycopg2
* SQLAlchemy
* sqlite3

## Introdução

Aplicações de software frequentemente precisam armazenar e consultar informações em bancos de dados. Para realizar essa comunicação, as linguagens de programação utilizam bibliotecas ou drivers que permitem estabelecer uma conexão entre a aplicação e o sistema gerenciador de banco de dados.

No Python existem diferentes bibliotecas para essa finalidade. Algumas são específicas para determinados bancos de dados, enquanto outras permitem trabalhar com diferentes sistemas.

Também existem diferenças na forma de interação com o banco. Algumas bibliotecas utilizam comandos SQL diretamente, enquanto outras oferecem recursos de ORM (Object-Relational Mapping), permitindo representar tabelas do banco de dados por meio de classes e objetos Python.

Neste trabalho serão apresentadas cinco bibliotecas utilizadas para conexão com bancos de dados relacionais, mostrando suas características e exemplos básicos de conexão e consulta.

---

# 1. pyodbc

## 1. Qual é o objetivo principal da biblioteca?

O `pyodbc` é uma biblioteca Python utilizada para conectar aplicações a bancos de dados através do padrão ODBC (Open Database Connectivity).

Seu objetivo é permitir que programas escritos em Python executem operações em bancos de dados, como consultas, inserções, alterações e exclusões de registros.

## 2. Que tipo de banco de dados ela permite acessar?

O `pyodbc` pode acessar diferentes sistemas de banco de dados que possuam um driver ODBC instalado no computador.

Alguns exemplos são:

* Microsoft SQL Server
* MySQL
* PostgreSQL
* Oracle
* Microsoft Access

A compatibilidade depende da existência de um driver ODBC adequado para o banco utilizado.

## 3. Ela é mais indicada para bancos relacionais ou não relacionais?

O `pyodbc` é principalmente utilizado com bancos de dados relacionais.

## 4. A biblioteca trabalha com SQL puro, ORM ou ambos?

O `pyodbc` trabalha principalmente com SQL puro.

Os comandos SQL são escritos diretamente pelo programador e enviados para o banco de dados através de um cursor.

Exemplo:

```python
cursor.execute("SELECT * FROM clientes")
```

O `pyodbc` não possui um ORM próprio.

## 5. Como é feita a instalação?

```bash
pip install pyodbc
```

Além da biblioteca, é necessário possuir o driver ODBC correspondente ao banco de dados utilizado.

## 6. Como é criado um exemplo simples de conexão?

```python
import pyodbc

conexao = pyodbc.connect(
    "DRIVER={ODBC Driver 18 for SQL Server};"
    "SERVER=localhost;"
    "DATABASE=empresa;"
    "UID=usuario;"
    "PWD=senha;"
    "TrustServerCertificate=yes;"
)

print("Conexão realizada com sucesso!")

conexao.close()
```

## 7. Como executar uma consulta SELECT simples?

```python
import pyodbc

conexao = pyodbc.connect(
    "DRIVER={ODBC Driver 18 for SQL Server};"
    "SERVER=localhost;"
    "DATABASE=empresa;"
    "UID=usuario;"
    "PWD=senha;"
    "TrustServerCertificate=yes;"
)

cursor = conexao.cursor()

cursor.execute("SELECT * FROM clientes")

registros = cursor.fetchall()

for registro in registros:
    print(registro)

cursor.close()
conexao.close()
```

---

# 2. pymssql

## 1. Qual é o objetivo principal da biblioteca?

O `pymssql` é uma biblioteca Python utilizada para realizar a comunicação entre aplicações Python e bancos de dados Microsoft SQL Server.

Ela fornece uma interface compatível com o padrão DB-API do Python, permitindo realizar operações no banco como consultas, inserções, atualizações e exclusões.

Diferente do `pyodbc`, que pode trabalhar com vários bancos através de drivers ODBC, o `pymssql` é desenvolvido especificamente para Microsoft SQL Server.

## 2. Que tipo de banco de dados ela permite acessar?

O `pymssql` é utilizado principalmente para acessar:

* Microsoft SQL Server
* Bancos SQL Server hospedados no Microsoft Azure

A biblioteca utiliza o protocolo TDS (Tabular Data Stream), através do FreeTDS, para realizar a comunicação com o SQL Server.

## 3. Ela é mais indicada para bancos relacionais ou não relacionais?

O `pymssql` é indicado para bancos de dados relacionais.

O Microsoft SQL Server utiliza o modelo relacional, em que os dados são organizados principalmente em tabelas compostas por linhas e colunas.

## 4. A biblioteca trabalha com SQL puro, ORM ou ambos?

O `pymssql` trabalha diretamente com comandos SQL.

Por exemplo:

```python
cursor.execute("SELECT * FROM clientes")
```

A biblioteca não possui um ORM próprio.

Caso seja necessário utilizar ORM, outras ferramentas podem ser utilizadas em conjunto, como o SQLAlchemy.

## 5. Como é feita a instalação?

A instalação pode ser realizada através do `pip`:

```bash
pip install pymssql
```

Também pode ser utilizado:

```bash
python -m pip install pymssql
```

Depois da instalação, a biblioteca pode ser importada no Python:

```python
import pymssql
```

## 6. Como é criado um exemplo simples de conexão?

Uma conexão simples com um Microsoft SQL Server pode ser realizada da seguinte forma:

```python
import pymssql

conexao = pymssql.connect(
    server="localhost",
    user="usuario",
    password="senha",
    database="empresa"
)

print("Conexão realizada com sucesso!")

conexao.close()
```

Neste exemplo:

* `server` representa o endereço do SQL Server;
* `user` representa o usuário utilizado na autenticação;
* `password` representa a senha;
* `database` representa o banco de dados que será acessado.

## 7. Como executar uma consulta SELECT simples?

Depois de estabelecer a conexão, podemos criar um cursor e utilizar o método `execute()` para executar o comando SQL.

```python
import pymssql

conexao = pymssql.connect(
    server="localhost",
    user="usuario",
    password="senha",
    database="empresa"
)

cursor = conexao.cursor()

cursor.execute("SELECT * FROM clientes")

registros = cursor.fetchall()

for registro in registros:
    print(registro)

cursor.close()
conexao.close()
```

O comando:

```python
cursor.execute("SELECT * FROM clientes")
```

envia a consulta SQL para o banco.

Já:

```python
cursor.fetchall()
```

recupera os registros retornados pela consulta.
