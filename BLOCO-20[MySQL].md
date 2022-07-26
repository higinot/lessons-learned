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

### INSERT
*Serve para inserir dados em uma tabela vazia*


### COUNT 
*Serve para contar a quantidade de casos em uma tabela*

>Conta todos os dados dentro do sakila.actor.
~~~javascript
SELECT COUNT (*) FROM sakila.actor ;
~~~

>Conta todos os dados da coluna first_name dentro da tabela sakila.andress
~~~javascript
SELECT COUNT(first_name) FROM sakila.actor ;
~~~

### LIMIT
*Serve para LIMITAR a quantidade de dados que é mostrado na visualização*

>Mostra os 10 primeiros dados da tabela sakila.rental
~~~javascript
SELECT * FROM sakila.rental LIMIT 10 ;
~~~

### LIMIT OFFSET
*Serve para limitar os dados em um intervalo*

> Mostra os 10 primeiros dados da tabela sakila.rental a partir da linha 4
~~~javascript
 SELECT * FROM sakila.rental LIMIT 10 OFFSET 3 ;
~~~

### ORDER BY
*Serve para ordenar o código de forma alfabética ou numerica, podendo ser de forma decrescente(DESC) ou crescente(ASC)*

> Mostra os dados da tabela sakila.address por ordenação ASC em district e DESC em address
~~~javascript
 SELECT * FROM sakila.address
 ORDER BY district ASC, address DESC; 
~~~

### WHERE
*Serve para filtrar a tabela de uma forma especifica*

> Seleciona os dados que tem os parâmetros que foram setados da tabela sakila.payment.

*Como o operador AND tem preferência sobre o operador OR,ele é avaliado primeiro*
~~~javascript
 SELECT * FROM sakila.payment
 WHERE amount = 0.99 OR amount = 2.99 AND staff_id = 2;
~~~

> Seleciona os dados que tem os parâmetros que foram setados da tabela sakila.payment.

*Primeiramente, a expressão dentro dos parênteses é avaliada, e todos os resultados que satisfazem a condição são retornados, na sequência, a expressão ao lado direito é avaliada.*
~~~javascript
SELECT * FROM sakila.payment
WHERE (amount = 0.99 OR amount = 2.99) AND staff_id = 2 ;
~~~

### LIKE
*Serve para selecionar os dados que conténham uma condição absoluta*

> Seleciona todos os dados da tabela sakila.film que terminam com don
~~~javascript
 SELECT * FROM sakila.film
 WHERE title LIKE '%don' ; 
~~~

* % - O sinal de percentual, que pode representar zero, um ou múltiplos caracteres
* _ - O underscore (às vezes chamado de underline, no Brasil), que representa um único caractere

> Seleciona todos os dados da tabela sakila.film que começam com plu
~~~javascript
SELECT * FROM sakila.film
WHERE title LIKE 'plu%' ;
~~~

> Seleciona qualquer resultado que inicia com p e finaliza com r
~~~javascript
SELECT * FROM sakila.film
WHERE title LIKE 'p%r' ;
~~~

> Seleciona qualquer resultado que o segundo caractere da frase é 'C'.
~~~javascript
SELECT * FROM sakila.film
WHERE title LIKE '_C%' ;
~~~

> Seleciona qualquer resultado que tenha 3 letras
~~~javascript
SELECT * FROM sakila.film
WHERE title LIKE '___'  ;
~~~

> Seleciona qualquer resultado que inicia com E e tenha no minino 3 caracteres.
~~~javascript
SELECT * FROM sakila.film
WHERE title LIKE 'E__%' ;
~~~ 

### IN
*Serve para substituir as condicionais AND ou OR*

> Seleciona todos os dados que satisfazem a condição IN 
~~~javascript
 SELECT * FROM sakila.actor
 WHERE first_name IN ('PENELOPE', 'NICK', 'ED','JENNIFER') ;
~~~

### BETWEEN
*Serve para selecionar dados em um intervalo especifico*

> Seleciona todos os dados que estão entre Italian e Mandarin
~~~javascript
 SELECT * FROM sakila.language
 WHERE name BETWEEN 'Italian' AND 'Mandarin'
 ORDER BY name ; 
~~~

### TRABALHANDO COM DATAS
*Códigos para trabalhar com seleção de datas no MySQL*

> Códigos
~~~javascript
 -- Teste cada um dos comandos a seguir:
SELECT DATE(payment_date) FROM sakila.payment; -- YYYY-MM-DD
SELECT YEAR(payment_date) FROM sakila.payment; -- Ano
SELECT MONTH(payment_date) FROM sakila.payment; -- Mês
SELECT DAY(payment_date) FROM sakila.payment; -- Dia
SELECT HOUR(payment_date) FROM sakila.payment; -- Hora
SELECT MINUTE(payment_date) FROM sakila.payment; -- Minuto
SELECT SECOND(payment_date) FROM sakila.payment; -- Segundo 
~~~

### INSERT
*Serve para inserir dados em uma tabela*

> Insere dados na coluna1 e coluna 2
~~~javascript
 INSERT INTO nome_da_tabela (coluna1, coluna2)
 VALUES ('valor_coluna1','valor_coluna2') ; 
~~~

> Insere multiplos dados na coluna 1 e coluna 2
~~~javascript
INSERT INTO nome_da_tabela (coluna1, coluna2)
VALUES
('valor_coluna1','valor_coluna2'),
('valor_coluna1','valor_coluna2'),
('valor_coluna1','valor_coluna2'),
('valor_coluna1','valor_coluna2'),
('valor_coluna1','valor_coluna2') ;
~~~

> Insere dados em uma tabela já existente

*Em casos que a tabela já possui AUTO_INCREMENT no id, não precisa colocar o id*
~~~javascript
INSERT INTO sakila.actos (first_name, last_name)
VALUES ('MARCELO','SANTOS') ;
~~~

### UPDATE
*Serve para atualizar valores existentem em uma tabela*

> A funçao UPDATE funciona de forma geral conforme o código abaixo
~~~javascript
UPDATE nome_da_tabela
SET propriedade_a_ser_alterada = 'novo valor para coluna'
WHERE alguma_condicao; -- importantíssimo aplicar o WHERE para não alterar a tabela inteira!
~~~

> Atualiza o first_name onde o first_name é Raiven
~~~javascript
 UPDATE sakila.staff
 SET first_name = 'Rannveing'
 WHERE fisrt_name = 'Ravein' ; 
~~~

> Atualiza o first_name e last_name onde o staff_id é igual a 4
~~~javascript
UPDATE sakila.staff
SET first_name = 'Rannveig', last_name = 'Jordan'
WHERE staff_id = 4 ;
~~~

> Fazendo atualizações em condições globais.
~~~javascript
-- Opção 1 - Incluindo a lista de condições fixas
UPDATE sakila.actor
SET first_name = 'JOE'
WHERE actor_id IN (1,2,3);

-- Opção 2 - Especificando como cada entrada será alterada individualmente
UPDATE sakila.actor
SET first_name = (
CASE actor_id WHEN 1 THEN 'JOE' -- se actor_id = 1, alterar first_name para 'JOE'
              WHEN 2 THEN 'DAVIS' -- se actor_id = 2, alterar first_name para 'DAVIS'
              WHEN 3 THEN 'CAROLINE' -- se actor_id = 3, alterar first_name para 'CAROLINE'
	      ELSE first_name -- em todos os outros casos, mantém-se o first_name
END);
~~~


### Criando uma TABELA:
    CREATE TABLE filme(  
        filme_id int NOT NULL PRIMARY KEY AUTO_INCREMENT COMMENT 'Primary Key',
        create_time DATETIME COMMENT 'Create Time',
        update_time DATETIME COMMENT 'Update Time',
        content VARCHAR(255) COMMENT 'content'
        ) DEFAULT CHARSET UTF8 COMMENT 'newTable';

