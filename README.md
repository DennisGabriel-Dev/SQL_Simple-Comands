# SQL_Simple-Comands
Nesse repositório mostro alguns comandos básicos de SQL , explicados de forma cronológica e lógica.


## Criar uma tabela 

 *No exemplo abaixo mostra como se cria uma tabela em SQL* <br>
 ```SQL
CREATE TABLE nomeDaTabela(
	NOME VARCHAR(150),
	ENDERECO VARCHAR(150),
	IDADE SMALLINT,
	FUNCIONARIO BIT(1),
	NASCIMENTO DATE
);
```
<br>
Você pode consultar mais formas de tipagem no site: 
<br>
https://learn.microsoft.com/pt-br/sql/t-sql/data-types/data-types-transact-sql?view=sql-server-ver16

## Inserir valores na tabela 

```SQL

USE nomeDoBanco; # USE --> esse comando é crucial, pois selecionamos o banco de dados com ele , antes de tudo.

INSERT INTO nomeDaTabela(
	NOME,
	ENDERECO,
	IDADE,
	FUNCIONARIO,
	NASCIMENTO
)VALUES(
	"Dennis",
	"Rua tal",
	19,
	0,
	"01-11-2002",
);
```

## Apagar uma tabela

```SQL

DROP TABLE nomeDaTabela;

```

## Apagar um elemento da tabela

```SQL

DELETE FROM nomeDaTabela WHERE IDADE = 19;

```

## Atualizar elemento(s) da tabela 

```SQL

UPDATE FROM nomeDaTabela SET IDADE =  20 WHERE IDADE = 19;

```

## Mostrar dados da tabela

```SQL
SELECT *  FROM nomeDaTabela; # Nesse caso,  todos os campos serão selecionados.

SELECT NOME , IDADE FROM nomeDaTabela ; # Nesse caso apenas o campo nome e idade serão selecionados.
```

## Limitar resultados
```SQL

SELECT *  FROM nomeDaTabela LIMIT 3; # Traz apenas os 3 primeiros elementos de acordo com a ordenação.

```
## Adiconar chave primária 

```SQL

ALTER TABLE nomeDaTabela ADD PRIMARY KEY(NOME); # O campo nome passa a ser a chave primária agora e 
com isso, não é mais possível adicionar nomes repetidos na tabela.

```


## Filtrar datas

```SQL
SELECT * FROM nomeDaTabela WHERE NASCIMENTO = '2002-11-01';

SELECT * FROM nomeDaTabela WHERE YEAR(NASCIMENTO) = 2002;
 
SELECT * FROM nomeDaTabela WHERE MONTH(NASCIMENTO) = 11;

SELECT * FROM nomeDaTabela WHERE DAY(NASCIMENTO) = 01;
```
