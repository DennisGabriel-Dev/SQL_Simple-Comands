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
#Poderia também ser mais específico e selecionar pelo nome:
UPDATE FROM nomeDaTabela SET IDADE =  20 WHERE NOME = "Dennis";

```

## Mostrar dados da tabela

```SQL
SELECT *  FROM nomeDaTabela; # Nesse caso,  todos os campos serão selecionados.

SELECT NOME , IDADE FROM nomeDaTabela ; # Nesse caso apenas o campo nome e idade serão selecionados.
```

## Limitar resultados
```SQL

SELECT *  FROM nomeDaTabela LIMIT 3; 
# Traz apenas os 3 primeiros elementos de acordo com a ordenação.

```
## Adiconar chave primária 

```SQL

ALTER TABLE nomeDaTabela ADD PRIMARY KEY(NOME); 
#O campo nome passa a ser a chave primária agora, com isso, não é mais possível adicionar nomes repetidos na tabela.

```


## Filtrar datas

```SQL
SELECT * FROM nomeDaTabela WHERE NASCIMENTO = '2002-11-01';

SELECT * FROM nomeDaTabela WHERE YEAR(NASCIMENTO) = 2002;
 
SELECT * FROM nomeDaTabela WHERE MONTH(NASCIMENTO) = 11;

SELECT * FROM nomeDaTabela WHERE DAY(NASCIMENTO) = 01;
```


## Filtrar resultados 
```SQL
SELECT * FROM nomeDaTabela WHERE idade = 19 ; #retorna apenas os resultados que possuem a idade IGUAL a 19.

SELECT * FROM nomeDaTabela WHERE idade > 19 ; #retorna apenas os resultados que possuem a idade MAIOR que 19.

SELECT * FROM nomeDaTabela WHERE idade < 19 ; #retorna apenas os resultados que possuem a idade MENOR que 19.

SELECT * FROM nomeDaTabela WHERE idade <> 19 ; #retorna apenas os resultados que NÃO possuem a idade igual a 19.
```
## Palavras AND e OR

```SQL
SELECT * FROM nomeDaTabela WHERE idade = 19 AND nome = "Dennis" ; 
#retorna apenas os resultados que possuem a idade igual a 19 "e" possuem nome Dennis.

SELECT * FROM nomeDaTabela WHERE (idade = 19 OR nome="Dennis") ;

# Retorna os resultados que tenham a idade igual a 19 "ou" que tenham o nome Dennis.
/*
Perceba que, coloquei parenteses para agrupar no último exemplo, 
eles não são necessários, mas que por boas práticas é importante, até mesmo para a nossa visualização.
*/
```


## Acrescentando novas colunas na tabela.
```SQL
ALTER TABLE nomeDaTabela ADD COLUMN nova_coluna VARCHAR(20) , nova_coluna2 FLOAT; 
#criamos duas colunas , uma q recebe texto e outra que recebe número inteiro
```

#### IMPORTANTE! Copie e execute tudo desse trecho, irei demonstrar uma coisa interessante mais a frente.
```SQL
INSERT INTO nomeDaTabela(NOME,ENDERECO,IDADE,FUNCIONARIO,NASCIMENTO,nova_coluna,nova_coluna2)
VALUES("Karol","Rio De Janeiro",21,0,"01-01-2001","teste",20.00);

INSERT INTO nomeDaTabela(NOME,ENDERECO,IDADE,FUNCIONARIO,NASCIMENTO,nova_coluna,nova_coluna2)
VALUES("Michel","Cuiabá",20,0,"01-01-2002","teste",150.00);

INSERT INTO nomeDaTabela(NOME,ENDERECO,IDADE,FUNCIONARIO,NASCIMENTO,nova_coluna,nova_coluna2)
VALUES("Samara","São Paulo",27,0,"19-06-1995","teste",90.00);

INSERT INTO nomeDaTabela(NOME,ENDERECO,IDADE,FUNCIONARIO,NASCIMENTO,nova_coluna,nova_coluna2)
VALUES("Francisco","Rio De Janeiro",45,0,"01-01-2001","teste",10.00);

```

## Alias 
```SQL
/*
Antes, colocamos as colunas na tabela: nova_coluna e nova_coluna2, porém elas não refletem uma boa comunicação,
diante disso, vamos nomear o nome desses campos no SELECT.
*/

SELECT NOME, ENDERECO, IDADE, FUNCIONARIO, NASCIMENTO, nova_coluna AS Tipo_de_Conta, nova_coluna2 AS Devendo FROM nomeDaTabela

#Agora quando executarmos o SELECT, as colunas virão com nomes diferentes, no  caso , nova_coluna passa a ser Tipo_De_Conta e nova_coluna2 passa a ser Devendo.
/*
Só que há um problema nessa abordagem, ela é visual e apenas temporária, precisamos colocar AS toda vez que desejarmos mudar o nome da(s) coluna(s) no SELECT.
A seguir, mostraremos como mudar o nome da tabela de fato.
*/
```

## Alterando o nome da(s) coluna(s)
```SQL
ALTER TABLE nomeDaTabela CHANGE nova_coluna Tipo_de_Conta VARCHAR(20) , CHANGE nova_coluna2 Devendo FLOAT;
/* Excelente, agora mudamos o nome das colunas: nova_coluna e nova_coluna2 de forma "permanente" através da palavra CHANGE.
*/
```

START TRANSACTION -  #Cria um ponto de estado do banco de dados. 
COMMIT -  Confirma todas as operações entre START TRANSACTION e o commit COMMIT. Todos os INSERTS, UPDATES OU DELETES irão ser confirmados e gravados na base
ROLLBACK: Tudo que foi feito entre o START TRANSACTION e o ROLLBACK será desprezado e os dados voltarão ao status de quando o START TRANSACTION foi executado 

