# mysql-001-a-controle-compras

Anotações do curso de MySQL.

##### Anotações:

1 - Não se esqueça do ";" no final das querys.

2 - Entrar no mysql instalado na maquina:
    mysql -u root -p;

3 - Criar e acessa o banco de dados:
    CREATE DATABASE controle_compras;
    use controle_compras;

4 - Criar uma tabela:
    CREATE TABLE compras (id INT AUTO_INCREMENT PRIMARY KEY, valor DOUBLE, data DATE, observacoes VARCHAR(255), recebido BOOLEAN);

5 - Inserir na tabela compras:
    INSERT INTO compras (valor, data, observacoes, recebido) VALUES (100.0, '2007-05-12', 'Compras de Maio', 1);

6 - Busca todo o conteudo da tabela:
    SELECT * FROM compras;

7 - Pega as instuções SQL no arquivo e executa no banco de dados;
    mysql -uroot -p controle_compras < cap2.sql;

8 - Busca a coluna "valor", "valor" multiplicando por 3 e dando um apelido:
    SELECT valor, valor * 3 AS triplo FROM compras;

9 - Consulta com filtro:
    SELECT * FROM compras WHERE (valor > 1000 AND data <= '2017-01-01') OR valor <> 1000;

10 - Consulta fitrando por uma parte da String:
    SELECT * FROM compras WHERE observacoes LIKE 'compras%';

11 - Para importar SQLs deslogue do MySQL e execute:
    mysql -u root -p controle_compras < cap2.sql

12 - Pode usar aspas duplas no lugar de aspas simples.

13 - O BETWEEN serve para filtrar de acordo com um intervalo (int ou data).
    SELECT * FROM compras WHERE valor BETWEEN 200 AND 700

14 - Comando usado para alterar dados, e o comando NOT para negar condição fazendo pegar o contrario.
    UPDATE compras SET observacoes = 'compra emergencial', recebido = 0 WHERE id = 2 OR data NOT BETWEEN '2010-01-05' AND '2010-06-25';

15 - Pegando varios valores para um mesmo campo com IN.
    UPDATE compras SET observacoes = 'datas festivas' WHERE DATA IN('2017-12-25', '2017-10-12', '2017-06-12');

16 - Excluir registros antes de 2009.
    DELETE FROM compras WHERE DATA < '2009-01-01';

17 - Sempre faça um SELECT para testar o WHERE antes de usar o UPDATE ou DELETE.

18 - Fazer um coluna da tabela começar a recusar NULL.
    ALTER TABLE compras MODIFY COLUMN observacoes TEXT NOT NULL;

19 - Adicionar um valor padrão para uma coluna da tabela.
    ALTER TABLE compras MODIFY COLUMN recebido TINYINT(1) DEFAULT '0';

20 - Para definir valores especificos que uma coluna pode resceber vc pode usar o ENUM().
    ALTER TABLE compras ADD COLUMN forma_pagt ENUM('cartao', 'boleto', 'dinheiro');

21 - O comando CHANGE pode ser usado para renomear uma coluna.
    ALTER TABLE compras CHANGE forma_pagt forma_pagamento ENUM('CARTAO', 'BOLETO', 'DINHEIRO');

22 - Para ver as colunas de uma tabela use o DESC.
    DESC compras;

23 - Para comparar com nulo vc não usa o "=", mas sim a palavra IS.

24 - Somar todos os valores de uma coluna, agrupando as recebidas e ordenando.
    SELECT SUM(valor), recebido FROM compras GROUP BY recebido ORDER BY data DESC, recebido ASC;

25 - Exibir a média dos valores de uma coluna e dando um apelido com AS.
    SELECT AVG(valor) AS media FROM compras;

26 - Contar o numero de pagamentos.
    SELECT COUNT(valor) FROM compras;

27 - Para pegar o mes ou o ano de uma data.
    SELECT month(data), year(data) FROM compras;

28 - Use o JOIN para fazer uma junção dos dados de tabelas diferentes que tem relação entre si usando FKs.
    SELECT * FROM compras JOIN compradores ON compras.comprador_id = compradores.id;

29 - Uma PK é um id que identifica um registro e uma FK é uma ligação com outro registro, e criar uma FK evita ligações invalidas, como inserir um ID que não existe na outra tabela.

30 - Definindo uma FK.
    ALTER TABLE compras ADD FOREIGN KEY (comprador_id) REFERENCES compradores(id);

31 - Para iniciar o servidor do mysql na linha de comando, acesse a bin do server do mysql, e execute (atenção ao erro que informa que falta a pasta 'data'):
    mysqld
