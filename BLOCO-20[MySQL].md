# MySQL

*SQL (Structured Query Language) é a linguagem mais usada para criar, pesquisar, extrair e também manipular dados dentro de um banco de dados relacional. Para que isso seja possível, existem comandos como o SELECT, UPDATE, DELETE, INSERT e WHERE, entre outros, que você aprenderá ao longo do curso.*

## Constraints (Restrições):

*Como as constraints são aplicadas às colunas das tabelas, é possível assegurar que os dados inseridos nelas serão consistentes conforme as regras definidas. Veja alguns tipos de constraints:()*

* NOT NULL - Como as constraints são aplicadas às colunas das tabelas, é possível assegurar que os dados inseridos nelas serão consistentes conforme as regras definidas. Veja alguns tipos de constraints.

* UNIQUE - Garante que o valor inserido na coluna da tabela é único, isto é, não pode haver outro valor igual para esta coluna registrado nesta tabela.

* PRIMARY KEY - Garante 
que o valor seja a chave primária da tabela, ou seja, que a coluna que possui essa constraint aplicada seja o identificador único da tabela. Ela também é, por definição, não nula (mesmo efeito da constraint NOT NULL) e única (mesmo efeito da constraint UNIQUE).
* FOREIGN KEY - Garante que o valor seja uma chave estrangeira da tabela, ou seja, faça referência à chave primária (valor em uma coluna com a constraint PRIMARY KEY) de outra tabela, permitindo um relacionamento entre tabelas.

* DEFAULT - Garante que, caso nenhum valor seja inserido na coluna (ou caso a pessoa usuária insira um valor nulo), a constraint colocará o valor padrão passado para ela.


## Entidade

*Quando se fala de entidades de um banco de dados, estamos normalmente falando de uma tabela que representa algum conceito do mundo real que você quer descrever (pessoa, eventos, acontecimentos) e suas propriedades (altura, horário do evento, nome do acontecimento).*

* Entidade: Pessoas
* Propriedades: Altura, peso, idade.

## Conexão de dados

*Para não precisarmos duplicar dados em tabelas diferentes, podemos estabelecer relacionamentos entre as tabelas. Em um banco de dados existem quatro tipos de relacionamento.*

    -Um para Um: Uma linha da Tabela A só deve possuir uma linha correspondente na tabela B ou vice-versa. (1:1)

    -Um para Muitos ou Muitos para um: Uma linha na tabela A pode ter várias linhas correspondentes na tabela B, mas uma linha da tabela B só pode possuir uma linha correspondente na tabela A. (N:1) ou (1:N)

    - Muitos para Muitos: Uma linha na tabela A pode possuir muitas linhas correspondentes na tabela B e vice-versa. (N:N)

## Query (Queries)

*Inquirir, ou query, em inglês, é o nome dado aos comandos que você digita dentro de uma janela ou linha de comando com a intenção de interagir de alguma maneira com uma base de dados.*

* DDL: *Data Definition Language* - Todos os comandos que lidam com o esquema, a descrição e o modo como os dados devem existir em um banco de dados:
    
    * **CREATE**: Para criar bandcos de dados, tabelas, indices, views, procedures, functions e triggers.
    * **ALTER**: Para alterar a estrtutura de qualquer objeto.
    * **DROP**: Permite deletar objetos.
    * **TRUCATE**: Apenas esvazia os dados dentro de uma tabela, mas a mantém no banco de dados.

* **DML**: *Data Manipulation Language* - Comandos que são usados para manipular dados. São utilizados para armazenar, modificar, buscar e excluir dados em um banco de dados. Os comandos e ussos mais comuns nesta categoria são:
    
    * **SELECT**: Usado para buscar dados em um banco de dados.
    * **INSERT**: Insere dados em uma tabela.
    * **UPDATE**: Altera dados dentro de uma tabela.
    * **DELETE**: Exclui dados de uma tabela.

* **DCL**: *Data Control Language* - Mais focado nos comandos que concedem direitos, permissões e outros tipos de controle ao sistema de banco de dados.

    * **GRANT**: Concede acesso a um usuário.
    * **REVOKE**: Remove acessos concedidos através do comando GRANT.

* **TCL**: *Transactional Control Language* - Lida com as transações dentro de suas pesquisas.

    * **COMMIT**: Muda suas alterações de temporários para permanentes no seu banco de dados.
    * **ROLLBACK**: Desfaz tudo o impacto realizado por um comando.
    * **SAVEPOINT**: Define pontos para os quais uma transação pode voltar. É uma maneira de voltar para pontos especificos de sua query.
    * **TRANSACTION**: Comandos que definem onde, como e em que escopo suas transações são executadas.

## Comandos MySQL

### SELECT 
*Esses conceitos são usar o SELECT para gerar valores e usar o AS para dar nomes às suas colunas, como nos exemplos a seguir.*

    SELECT * FROM sakila.city - Seleciona todas colunas da tabela city ;

    SELECT city, country_id FROM sakila.city - Seleciona a coluna city e country_id da tabela city ;

    SELECT 'Rafael' AS nome, 'Martins' AS 'sobrenome' - Cria uma tabela com uma coluna nome / Rafael e uma sobrenome / Martins ;

### CONCAT 
*é possível concatenar mais de uma coluna em apenas uma. Para isso, usamos a função CONCAT, que cria novos dados e informações a partir dos dados já existentes em uma tabela.*

    SELECT CONCAT(first_name,' ', last_name) FROM sakila.actor ;

    SELECT CONCAT(first_name,' ', last_name) AS 'nome_completo' FROM sakila.actor ;

### DISTINCT 
*Serve para eliminar valores repetidos*

### Criando uma TABELA:
    CREATE TABLE filme(  
        filme_id int NOT NULL PRIMARY KEY AUTO_INCREMENT COMMENT 'Primary Key',
        create_time DATETIME COMMENT 'Create Time',
        update_time DATETIME COMMENT 'Update Time',
        content VARCHAR(255) COMMENT 'content'
        ) DEFAULT CHARSET UTF8 COMMENT 'newTable';
