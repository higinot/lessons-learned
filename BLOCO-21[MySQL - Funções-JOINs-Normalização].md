# MySQL

*Texto sobre as principais funções em MySQL que lidam com números,strings, datas e agregação de dados no MySQL*

## Manipuçação de STRING's

> Principais podem ser vistas a seguir:
~~~javascript
-- Converte o texto da string para CAIXA ALTA
SELECT UCASE('Oi, eu sou uma string');

-- Converte o texto da string para caixa baixa
SELECT LCASE('Oi, eu sou uma string');

-- Substitui as ocorrências de uma substring em uma string
SELECT REPLACE('Oi, eu sou uma string', 'string', 'cadeia de caracteres');

-- Retorna a parte da esquerda de uma string de acordo com o
-- número de caracteres especificado
SELECT LEFT('Oi, eu sou uma string', 3);

-- Retorna a parte da direita de uma string de acordo com o
-- número de caracteres especificado
SELECT RIGHT('Oi, eu sou uma string', 6);

-- Exibe o tamanho, em caracteres, da string, a função LENGTH retorna o tamanho em bytes
SELECT CHAR_LENGTH('Oi, eu sou uma string');

-- Extrai parte de uma string de acordo com o índice de um caractere inicial
-- e a quantidade de caracteres a extrair
SELECT SUBSTRING('Oi, eu sou uma string', 5, 2);

-- Se a quantidade de caracteres a extrair não for definida,
-- então a string será extraída do índice inicial definido, até o seu final
SELECT SUBSTRING('Oi, eu sou uma string', 5);
~~~

## Condicionais

> Utilização do IF em MySQL
~~~javascript
-- Sintaxe:
SELECT IF(condicao, valor_se_verdadeiro, valor_se_falso);

SELECT IF(idade >= 18, 'Maior de idade', 'Menor de Idade')
FROM pessoas;

SELECT IF(aberto, 'Entrada permitida', 'Entrada não permitida')
FROM estabelecimentos;

-- Exemplo utilizando o banco sakila:
SELECT first_name, IF(active, 'Cliente Ativo', 'Cliente Inativo') AS status
FROM sakila.customer
LIMIT 20;
~~~

> Utilização do CASE em MySQL
~~~javascript
-- Sintaxe:
SELECT CASE
  WHEN condicao THEN valor
  ELSE valor padrao
END;

SELECT
    nome,
    nivel_acesso,
    CASE
        WHEN nivel_acesso = 1 THEN 'Nível de acesso 1'
        WHEN nivel_acesso = 2 THEN 'Nível de acesso 2'
        WHEN nivel_acesso = 3 THEN 'Nível de acesso 3'
        ELSE 'Usuário sem acesso'
    END AS nivel_acesso
FROM permissoes_usuario;

-- Exemplo utilizando a tabela sakila.film:
SELECT
    first_name,
    email,
    CASE
        WHEN email = 'MARY.SMITH@sakilacustomer.org' THEN 'Cliente de baixo valor'
        WHEN email = 'PATRICIA.JOHNSON@sakilacustomer.org' THEN 'Cliente de médio valor'
        WHEN email = 'LINDA.WILLIAMS@sakilacustomer.org' THEN 'Cliente de alto valor'
        ELSE 'não classificado'
    END AS valor
FROM sakila.customer
LIMIT 10;
~~~

## Funções Matemáticas do MySQL

> Funções básicas em MySQL
~~~javascript
SELECT 5 + 5;
SELECT 5 - 5;
SELECT 5 * 5;
SELECT 5 / 5;
~~~

> Funções básicas usando tabalas
~~~javascript
SELECT rental_duration + rental_rate FROM sakila.film LIMIT 10;
SELECT rental_duration - rental_rate FROM sakila.film LIMIT 10;
SELECT rental_duration / rental_rate FROM sakila.film LIMIT 10;
SELECT rental_duration * rental_rate FROM sakila.film LIMIT 10;
~~~

> Divisão de inteiros com DIV
~~~javascript
SELECT 10 DIV 3; -- 3
SELECT 10 DIV 2; -- 5
SELECT 14 DIV 3; -- 4
SELECT 13 DIV 2; -- 6
~~~

> Resto da divisão com MOD
~~~javascript
SELECT 10 MOD 3; -- 1
SELECT 10 MOD 2; -- 0
SELECT 14 MOD 3; -- 2
SELECT 13 MOD 2; -- 1
SELECT 10.5 MOD 2; -- 0.5, ou seja, 2 + 2 + 2 + 2 + 2 = 10, restando 0.5
~~~

## Trabalhando com datas

> Conseguimos consultar data e hora atuais utilizando as seguintes funções
~~~javascript
SELECT CURRENT_DATE(); -- 'YYYY-MM-DD'
SELECT NOW(); -- 'YYYY-MM-DD HH:MM:SS'
~~~


> Podemos também calcular a diferença entre dois horarios,datas.
~~~javascript
-- 30, ou seja, a primeira data é 30 dias depois da segunda
SELECT DATEDIFF('2020-01-31', '2020-01-01');

-- -30, ou seja, a primeira data é 30 dias antes da segunda
SELECT DATEDIFF('2020-01-01', '2020-01-31');

-- -01:00:00, ou seja, há 1 hora de diferença entre os horários
SELECT TIMEDIFF('08:30:10', '09:30:10');

-- -239:00:00, ou seja, há uma diferença de 239 horas entre as datas
SELECT TIMEDIFF('2021-08-11 08:30:10', '2021-08-01 09:30:10');
~~~

## Funções de agregação 

*Funções que analisam todos os registros de uma determinada coluna e retornam um valor depois de comparar e avaliar todos os registros*

> Utilizando a coluna replacement_cost (valor de sustituição), vamor encontrar:
~~~javascript
-- Usando a coluna replacement_cost (valor de substituição), vamos encontrar:
SELECT AVG(replacement_cost) FROM sakila.film; -- 19.984000 (Média entre todos registros)
SELECT MIN(replacement_cost) FROM sakila.film; -- 9.99 (Menor valor encontrado)
SELECT MAX(replacement_cost) FROM sakila.film; -- 29.99 (Maior valor encontrado)
SELECT SUM(replacement_cost) FROM sakila.film; -- 19984.00 (Soma de todos registros)
SELECT COUNT(replacement_cost) FROM sakila.film; -- 1000 registros encontrados (Quantidade)
~~~

## Filtrando de forma agrupada com GROUP BY e HAVING


> O GROUP BY pode ser construido da seguinte forma:
~~~javascript
SELECT coluna(s) FROM tabela
GROUP BY coluna(s);
~~~

> Alguns códigos utilizando a diretriz de GROUP BY
~~~javascript
-- Média de duração de filmes agrupados por classificação indicativa
SELECT rating, AVG(length)
FROM sakila.film
GROUP BY rating;

-- Valor mínimo de substituição dos filmes agrupados por classificação indicativa
SELECT rating, MIN(replacement_cost)
FROM sakila.film
GROUP BY rating;

-- Valor máximo de substituição dos filmes agrupados por classificação indicativa
SELECT rating, MAX(replacement_cost)
FROM sakila.film
GROUP BY rating;

-- Custo total de substituição de filmes agrupados por classificação indicativa
SELECT rating, SUM(replacement_cost)
FROM sakila.film
GROUP by rating;
~~~


> Podemos utilizar o HAVING para filtrar resultados agrupados, assim como usamos o SELECT...WHERE para filtrar resultados individuais.
~~~javascript
SELECT first_name, COUNT(*)
FROM sakila.actor
GROUP BY first_name
HAVING COUNT(*) > 2;

-- Ou, melhor ainda, usando o AS para dar nomes às colunas de agregação,
-- melhorando a leitura do resultado
SELECT first_name, COUNT(*) AS nomes_cadastrados
FROM sakila.actor
GROUP BY first_name
HAVING nomes_cadastrados > 2;

-- Observação: o alias não funciona com strings para o HAVING,
-- então use o underline ("_") para separar palavras
-- Ou seja, o exemplo abaixo não vai funcionar
SELECT first_name, COUNT(*) AS 'nomes cadastrados'
FROM sakila.actor
GROUP BY first_name
HAVING 'nomes cadastrados' > 2;
~~~

## JOIN

*A ideia do JOIN é permitir combinar registros de duas ou mais tabelas, através do relacionamento que uma tabela tem com a outra.*

*Essa funcionalidade pode ser usadas para diferentes propósitos no seu dia a dia de trabalho, como a criação de relatórios, de novas maneiras de exibir uma informação já cadastrada em uma tabela e adicionar detalhes a tabelas existentes, entre outras possibilidades.*

> A sintaxe para o INNER JOIN é a seguinte
~~~javascript
SELECT t1.coluna, t2.coluna
FROM tabela1 AS t1
INNER JOIN tabela2 AS t2
ON t1.coluna_em_comum = t2.coluna_em_comum;
~~~

### LEFT JOIN & RIGHT JOIN
*Você precisa encontrar um conjunto de registros, mas não tem certeza se uma das colunas de referência envolvidas possui ou não essa informação*

> LEFT JOIN - *quando utilizamos o LEFT JOIN, focamos a tabela da esquerda. São retornados todos os registros da tabela da esquerda e valores correspondentes da tabela da direita, caso existam. Valores que não possuem correspondentes são exibidos como nulos.*
~~~javascript
 SELECT
    c.customer_id,
    c.first_name,
    c.last_name,
    a.actor_id,
    a.first_name,
    a.last_name
FROM sakila.customer AS c
LEFT JOIN sakila.actor AS a
ON c.last_name = a.last_name
ORDER BY c.last_name; 
~~~
![LEFT JOIN](https://assets.app.betrybe.com/back-end/sql/images/leftjoin-3bd116be2c7d08ac759c74353260cfea.png)
> RIGHT JOIN - *uando utilizamos o RIGHT JOIN, focamos a tabela da direita. São retornados todos os registros da tabela da direita e valores correspondentes da tabela da esquerda, caso existam. Valores que não possuem correspondentes são exibidos como nulos.*
~~~javascript
SELECT
    c.customer_id,
    c.first_name,
    c.last_name,
    a.actor_id,
    a.first_name,
    a.last_name
FROM sakila.customer AS c
RIGHT JOIN sakila.actor AS a
ON c.last_name = a.last_name
ORDER BY c.last_name;
~~~
![RIGHT JOIN](https://assets.app.betrybe.com/back-end/sql/images/rightjoin-f8109b9bb4ea1ed927109d1e19a1a262.png)


> INNER JOIN - *finalmente, temos o INNER JOIN, que foca em trazer somente os registros que possuem valores correspondentes em ambas as tabelas.*
~~~javascript
SELECT
    c.customer_id,
    c.first_name,
    c.last_name,
    a.actor_id,
    a.first_name,
    a.last_name
FROM sakila.customer AS c
INNER JOIN sakila.actor AS a
ON c.last_name = a.last_name
ORDER BY c.last_name;
~~~
![INNER JOIN](https://assets.app.betrybe.com/back-end/sql/images/innerjoin-dcdd0d7b81d1843386871875fc408dd4.png)

## Database Design

1. Identificar as entidades, atributos e relacionamentos com base na descrição do problema: Por exemplo, a entidade álbum possui os atributos título e preço e se relaciona com a entidade artista.

2. Construir um diagrama entidade-relacionamento para representar as entidades encontradas no passo 1: O diagrama serve como um guia para que você possa visualizar as entidades (tabelas) que irão se relacionar.

3. Criar um banco de dados para conter suas tabela: Após analisar e criar um diagrama de como o seu banco de dados vai ser estruturado, você pode dar início a criação dele.

4. Criar e relacionar tabelas tendo o diagrama do passo 2 como base: Após criar seu banco de dados, você pode começar a criar e relacionar as tabelas de acordo com o diagrama.

#### 1. Identificando entidades, atributos e relacionamentos

**Entidades**: São uma representação de algo do mundo real dentro do banco de dados e que normalmente englobalm toda uma ideia. São armazenados em formato de tabelas em um banco de dados.

*  `Entidade 1: Album`
*  `Entidade 2: Artista`
*  `Entidade 3: Estilo Musical`
*  `Entidade 4: Canção`

**Atributos**: *Um atributo é tudo aquilo que podes ser usado para descrever algo. Por exemplo, uma entidade pessoa pode ter nome, altura,peso e idade como atributos*

*  `Album: album_id, titulo, preco, estilo_id, artista_id`
*  `Artista: artista_id e nome `
*  `Estilo: estilo_id e nome`
*  `Cancao: cancao_id, nome e album_id`

**Relacionamentos**: *Os relacionamentos servem para representar como uma entidade deve estar ligada com outros(s) no banco de dados. Há três tipos de relacionamentos possíveis em um banco de dados, são eles:*

*  `Relacionamento Um para Um: (1..1)`
>Nesse tipo de relacionamento, uma lista da Tabela A deve possuir apenas uma linha correspondente da Tabela B e vice-virssa.

![1:1](https://assets.app.betrybe.com/back-end/sql/images/relacionamentos1.2-7e92dc1947281a68817caf5a53c014a5.png)


