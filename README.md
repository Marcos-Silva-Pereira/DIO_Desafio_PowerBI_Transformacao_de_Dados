# DIO - Desafio de projeto "Processando e Transformando Dados com Power BI"

Projeto de Power BI do Bootcamp Santander 2023 - Ciência de Dados com Python da DIO

# Objetivo

O objetivo é fazer uma integração do Power BI com um Banco de Dados e a transformação dos dados no Power Query, finalizando com um relatório mostrando informações relevantes.

# Descrição

Foi criado uma instância Mysql na Azure, e foi criado o banco de dados e as tabelas, e preenchido com informações fictícias. Em seguida foi feita a integração do Power BI com o banco de dados criado na Azure. Com as tabelas do banco de dados no Power BI, foi iniciado o processo de Transformação de dados no Power Query, seguindo um "roteiro". Finalizado as transformações de dados, foi montado um relatório mostrando as informações relevantes.

# Roteiro para a Transformação de Dados

    1. Verifique os cabeçalhos e tipos de dados
	    . Na tabela "departament" na coluna "Mgr_ssn" foi alterado o tipo de "texto" para "inteiro". 
	    . Na tabela "dependent" coluna "Essn", foi alterado o tipo "texto" para "inteiro".
	    . Na tabela "employee" foi feito a mesma coisa, com a coluna "ssn" e "Super_ssn". 
	    . Na tabela "works_on" coluna "Essn", tambem foi feito essa alteração do tipo da coluna de "texto" para "inteiro".
	
    2. Modifique os valores monetários para o tipo double preciso
	    . Na tabela "employee" na coluna "Salary", foi alterado o tipo de "inteiro" para "numero decimal fixo".

    3. Verifique a existência dos nulos e analise a remoção
        . Na tabela "employee" na coluna "Super_ssn" há a existencia de um nulo, porem ele não pode ser removido. 

    4. Os employees com nulos em Super_ssn podem ser os gerentes
        . Esse é o caso do unico nulo encontrado, ele é o gerente, portanto o "nulo" foi substituido por "0".

    5. Verifique se há algum colaborador sem gerente
        . Somente o colaborador "James", pois ele é o gerente.

    6. Verifique se há algum departamento sem gerente
        . Não, todos departamentos possuem gerentes relacionados.

    7. Se houver departamento sem gerente, suponha que você possui os dados e preencha as lacunas
        . Todos possuem gerentes.

    8. Verifique o número de horas dos projetos
        . Alguns projetos estão zerados, enquantos outros tem uma sobrecarga. Amaioria dos projetos tem de 10 a 20 horas, enquanto 4 projetos tem de 30 a 40 horas.

    9. Separar colunas complexas
        . A coluna "Address" na tabela "employee", foi dividida em "bairro_cidade", "numero" e "estado".

    10. Mesclar consultas employee e departament para criar uma tabela employee com o nome dos departamentos associados aos colaboradores. A mescla terá como base a tabela employee.
        OBS: fique atento, essa informação influencia no tipo de junção
        . Mesclar é parecido com o join do SQL.
        . A diferença de Mesclar consultas e de Combinar consultas, é que Mesclar consultas serve para quando queremos unir colunas, e Combinar para quando queremos unir a partir das linhas. O combinar não foi usado porque precisavamos de colunas especificas das duas tabelas.

    11. Neste processo elimine as colunas desnecessárias.
        . Utilizando a função Mesclar, foi mesclado as duas tabelas: "employee" e "departament". Foi utilizado a junção "externa esquerda".
        . Foi criado a tabela "employee_departament", contendo o nome, ssn, salario e o departamento do funcionário.

    12. Realize a junção dos colaboradores e respectivos nomes dos gerentes. Isso pode ser feito com consulta SQL ou pela mescla de tabelas com Power BI. Caso utilize SQL, especifique no README a query utilizada no perocesso.
        . Foi mesclado a tabela "employee" com a tabela "employee", assim utilizando o "Super_ssn" para fazer a junção entre os colaboradores e seus respectivos gerentes. A junção feita foi a "externa esquerda".

    13. Mescle as colunas de Nome e Sobrenome para ter apenas uma coluna definindo os nomes dos colaboradores.
        . Foi criado a tabela "employee_gerente", com a coluna "nome" sendo a junção das colunas "Fname", "Minit" e "Lname", e a coluna "Gerentes". 

    14. Mescle os nomes de departamentos e localizacao. Isso fará que cada combinação departamento-local seja único. Isso irá auxiliar na criação do modelo estrela em um módulo futuro.
        . Foi Mesclado as tabelas "departament" e "dept_location", atraves da junção "externa esquerda" utilizando o numero dos departamentos. A nova tabela "departamento_local", possui as colunas "Escritorio" (mescla das colunas "Dname" e "Dlocation"), "Dnumber" e "Mgr_ssn".

    15. Explique por que, neste caso supracitado, podemos apenas utilizar o mesclar e não o atribuir.
        . Porque o atribuir iria apenas acrescentar as linhas da segunda tabela abaixo das linhas da primeira tabela, e isso não iria atingir o nosso objetivo de associar o nome dos locais ao dos departamentos. 

    16. Agrupe os dados a fim de saber quantos colaboradores existem por gerente
        . Foi criado a tabela "colaboradores_por_gerentes", com as coluna "gerentes" e a coluna "qtd_colaboradores".

    17. Elimine as colunas desnecessárias, que não serão usadas no relatório, de cada tabela.
