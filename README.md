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

# 3. psycopg2

## 1. Qual é o objetivo principal da biblioteca?

O `psycopg2` é uma biblioteca Python utilizada para conectar aplicações ao banco de dados PostgreSQL.

Ela permite que programas escritos em Python executem operações no banco, como consultas, inserções, atualizações e exclusões de dados.

A biblioteca segue o padrão DB-API 2.0 do Python e utiliza a biblioteca `libpq`, que é o cliente oficial do PostgreSQL.

## 2. Que tipo de banco de dados ela permite acessar?

O `psycopg2` é desenvolvido especificamente para trabalhar com:

* PostgreSQL

Diferente do `pyodbc`, que pode trabalhar com diferentes bancos por meio de drivers ODBC, o `psycopg2` é voltado especificamente para PostgreSQL.

## 3. Ela é mais indicada para bancos relacionais ou não relacionais?

O `psycopg2` é indicado para bancos de dados relacionais.

O PostgreSQL é um sistema gerenciador de banco de dados relacional que utiliza SQL para criação, consulta e manipulação dos dados.

## 4. A biblioteca trabalha com SQL puro, ORM ou ambos?

O `psycopg2` trabalha diretamente com SQL.

Os comandos SQL são escritos pelo programador e executados utilizando um cursor.

Exemplo:

```python
cursor.execute("SELECT * FROM clientes")
```

O `psycopg2` não possui um ORM próprio.

Caso seja necessário utilizar ORM, ele pode ser utilizado em conjunto com outras ferramentas, como o SQLAlchemy.

## 5. Como é feita a instalação?

Para uma instalação simples, principalmente para estudo e desenvolvimento, pode ser utilizado:

```bash
pip install psycopg2-binary
```

Depois disso, a biblioteca é importada normalmente com:

```python
import psycopg2
```

Também é possível instalar a versão compilada a partir do código-fonte:

```bash
pip install psycopg2
```

A versão `psycopg2-binary` é mais simples de instalar porque já contém os componentes necessários para utilização da biblioteca.

## 6. Como é criado um exemplo simples de conexão?

Uma conexão com PostgreSQL pode ser feita utilizando o método `connect()`:

```python
import psycopg2

conexao = psycopg2.connect(
    host="localhost",
    database="empresa",
    user="postgres",
    password="senha"
)

print("Conexão realizada com sucesso!")

conexao.close()
```

Neste exemplo:

* `host` representa o endereço do servidor;
* `database` representa o banco de dados;
* `user` representa o usuário;
* `password` representa a senha de acesso.

O método `psycopg2.connect()` cria uma nova sessão com o banco de dados PostgreSQL.

## 7. Como executar uma consulta SELECT simples?

Depois de criar a conexão, é necessário criar um cursor para executar os comandos SQL.

Exemplo:

```python
import psycopg2

conexao = psycopg2.connect(
    host="localhost",
    database="empresa",
    user="postgres",
    password="senha"
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

executa a consulta SQL.

Depois:

```python
cursor.fetchall()
```

recupera todos os registros retornados pela consulta.

Também é possível recuperar apenas um registro utilizando:

```python
cursor.fetchone()
```
# 4. SQLAlchemy

## 1. Qual é o objetivo principal da biblioteca?

O `SQLAlchemy` é uma biblioteca Python utilizada para facilitar o acesso e a manipulação de bancos de dados relacionais.

Seu principal objetivo é fornecer ferramentas para trabalhar com bancos de dados de forma mais organizada, permitindo tanto a execução de comandos SQL quanto o uso de ORM (Object-Relational Mapping).

Com ORM, é possível representar tabelas do banco de dados através de classes Python e os registros através de objetos.

## 2. Que tipo de banco de dados ela permite acessar?

O SQLAlchemy pode trabalhar com diferentes bancos de dados relacionais.

Alguns exemplos são:

* SQLite
* PostgreSQL
* MySQL
* MariaDB
* Microsoft SQL Server
* Oracle

Para alguns desses bancos, é necessário instalar também um driver específico.

Por exemplo, para PostgreSQL pode ser utilizado um driver como o `psycopg2`.

## 3. Ela é mais indicada para bancos relacionais ou não relacionais?

O SQLAlchemy é indicado principalmente para bancos de dados relacionais.

Ele foi desenvolvido para trabalhar com bancos baseados em SQL e permite representar tabelas, colunas e relacionamentos por meio de objetos Python.

## 4. A biblioteca trabalha com SQL puro, ORM ou ambos?

O SQLAlchemy permite trabalhar de ambas as formas.

Ele possui dois componentes principais:

### SQLAlchemy Core

Permite trabalhar de forma mais próxima ao SQL e construir consultas utilizando objetos Python.

Também é possível executar comandos SQL textuais.

Exemplo:

```python
from sqlalchemy import text

resultado = conexao.execute(
    text("SELECT * FROM clientes")
)
```

### SQLAlchemy ORM

Permite representar tabelas como classes Python.

Por exemplo:

```python
class Cliente:
    nome = "João"
```

Em um projeto real, essa classe seria mapeada para uma tabela do banco de dados.

Portanto, o SQLAlchemy permite trabalhar tanto com SQL quanto com ORM.

## 5. Como é feita a instalação?

A instalação pode ser realizada utilizando o `pip`:

```bash
pip install SQLAlchemy
```

Também pode ser utilizado:

```bash
python -m pip install SQLAlchemy
```

Dependendo do banco utilizado, pode ser necessário instalar também um driver específico.

## 6. Como é criado um exemplo simples de conexão?

Para um exemplo simples, podemos utilizar um banco SQLite.

```python
from sqlalchemy import create_engine

engine = create_engine("sqlite:///empresa.db")

with engine.connect() as conexao:
    print("Conexão realizada com sucesso!")
```

Nesse exemplo:

```python
create_engine("sqlite:///empresa.db")
```

cria um objeto responsável pela comunicação com o banco `empresa.db`.

O `engine.connect()` cria a conexão que será utilizada para executar operações no banco.

## 7. Como executar uma consulta SELECT simples?

Uma consulta simples pode ser realizada utilizando `text()` e `execute()`.

```python
from sqlalchemy import create_engine, text

engine = create_engine("sqlite:///empresa.db")

with engine.connect() as conexao:

    resultado = conexao.execute(
        text("SELECT * FROM clientes")
    )

    for registro in resultado:
        print(registro)
```

Neste exemplo:

```python
text("SELECT * FROM clientes")
```

representa o comando SQL que será executado.

Já:

```python
conexao.execute(...)
```

envia a consulta para o banco de dados e retorna os resultados.

O SQLAlchemy também permite criar consultas utilizando sua própria estrutura de objetos através da função `select()`, sem precisar escrever toda a consulta manualmente.

# 5. sqlite3

## 1. Qual é o objetivo principal da biblioteca?

O `sqlite3` é um módulo do Python utilizado para acessar e manipular bancos de dados SQLite.

Seu objetivo é permitir que aplicações Python executem operações como criação de tabelas, inserção, atualização, exclusão e consulta de dados utilizando comandos SQL.

Uma das principais características do SQLite é que ele não precisa de um servidor de banco de dados separado. O banco pode ser armazenado diretamente em um arquivo no computador.

## 2. Que tipo de banco de dados ela permite acessar?

O módulo `sqlite3` permite acessar bancos de dados SQLite.

Um banco SQLite normalmente é armazenado em um único arquivo, por exemplo:

```text
empresa.db
```

Também é possível criar um banco temporário somente na memória utilizando:

```python
sqlite3.connect(":memory:")
```

## 3. Ela é mais indicada para bancos relacionais ou não relacionais?

O `sqlite3` é indicado para bancos de dados relacionais.

O SQLite organiza os dados principalmente em tabelas compostas por linhas e colunas e utiliza SQL para consultar e manipular essas informações.

## 4. A biblioteca trabalha com SQL puro, ORM ou ambos?

O `sqlite3` trabalha diretamente com SQL.

Os comandos são escritos pelo programador e executados através de um cursor.

Exemplo:

```python
cursor.execute("SELECT * FROM clientes")
```

O módulo `sqlite3` não possui um ORM próprio.

Caso seja necessário utilizar ORM com SQLite, é possível utilizar outras bibliotecas, como o SQLAlchemy.

## 5. Como é feita a instalação?

Normalmente não é necessário instalar o `sqlite3` através do `pip`, pois ele já faz parte da biblioteca padrão do Python.

Para utilizá-lo, basta importar o módulo:

```python
import sqlite3
```

Em uma instalação padrão do Python, o módulo já estará disponível.

## 6. Como é criado um exemplo simples de conexão?

Uma conexão pode ser criada utilizando o método `sqlite3.connect()`.

```python
import sqlite3

conexao = sqlite3.connect("empresa.db")

print("Conexão realizada com sucesso!")

conexao.close()
```

O comando:

```python
sqlite3.connect("empresa.db")
```

abre uma conexão com o arquivo `empresa.db`.

Caso o arquivo ainda não exista, o SQLite cria o banco de dados automaticamente.

## 7. Como executar uma consulta SELECT simples?

Depois de estabelecer a conexão, podemos criar um cursor e executar uma consulta SQL.

```python
import sqlite3

conexao = sqlite3.connect("empresa.db")

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

executa a consulta no banco.

Depois:

```python
cursor.fetchall()
```

recupera todos os registros retornados pela consulta.

Também é possível percorrer diretamente o resultado:

```python
for registro in cursor.execute("SELECT * FROM clientes"):
    print(registro)
```

