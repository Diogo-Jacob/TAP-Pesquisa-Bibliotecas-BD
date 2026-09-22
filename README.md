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

Isso ocorre porque bancos relacionais trabalham normalmente com SQL e possuem ampla compatibilidade com drivers ODBC.

## 4. A biblioteca trabalha com SQL puro, ORM ou ambos?

O `pyodbc` trabalha principalmente com SQL puro.

Os comandos SQL são escritos diretamente pelo programador e enviados para o banco de dados através de um cursor.

Por exemplo:

```python
cursor.execute("SELECT * FROM clientes")
```

O `pyodbc` não possui um ORM próprio.

## 5. Como é feita a instalação?

A instalação pode ser realizada utilizando o `pip`:

```bash
pip install pyodbc
```

Ou:

```bash
python -m pip install pyodbc
```

Além da biblioteca, é necessário possuir o driver ODBC correspondente ao banco de dados que será utilizado.

## 6. Como é criado um exemplo simples de conexão?

Um exemplo de conexão com um banco Microsoft SQL Server pode ser feito da seguinte forma:

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

Nesse exemplo:

* `DRIVER` informa qual driver ODBC será utilizado;
* `SERVER` informa o endereço do servidor;
* `DATABASE` informa o banco que será acessado;
* `UID` informa o usuário;
* `PWD` informa a senha.

## 7. Como executar uma consulta SELECT simples?

Primeiro é criado um cursor a partir da conexão. Depois, o comando SQL pode ser executado utilizando o método `execute()`.

Exemplo:

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

Nesse código, o comando:

```python
cursor.execute("SELECT * FROM clientes")
```

executa a consulta no banco de dados.

Já:

```python
cursor.fetchall()
```

recupera todos os registros retornados pela consulta.
