# Processando e Transformando Dados com Power BI - DIO Lab
Repositório do lab "Processando e Transformando Dados com Power BI" da DIO.

## Etapas iniciais do desafio

1. Criação de uma instância na Azure para MySQL

2. Criação do Banco de dados com a base disponível no [github](https://github.com/julianazanelatto/power_bi_analyst/tree/main/M%C3%B3dulo%203/Desafio%20de%20Projeto)

3. Integração do Power BI com MySQL no Azure

4. Verificação de problemas na base a fim de realizar a transformação dos dados

## Transformações e verificações

1. Verificação dos cabeçalhos e dos tipos de dados
2. Remoção das colunas de todas as tabelas que representam outra tabela
3. Verificação do número de horas dos projetos, há projetos com 0 horas
4. `employee.Salary` transformado de número decimal para `número decimal fixo`
5. Verificação de valores nulos, onde foi encontrado o colaborador de `employee.Ssn = 888665555` com `employee.Super_ssn = null`
6. O colaborador acima tem `Super_ssn` nulo, mas é gerente dos colaboradores de `employee.Ssn = 333445555 e 987654321`

   5.1 Consulta realizada: mesclagem da tabela `employee` consigo mesma onde `Ssn = Super_Ssn`, com junção externa esquerda)
7. Apenas o colaborador mencionado acima não tem um gerente associado.
8. Não há departamentos sem gerente, pois `departament.Mgr_ssn` não tem nenhum valor nulo
9. Divisão da coluna `employee.Address` em 4 campos: `Number`, `Street`, `City` e `State`, divididos pelo delimitador hífen (-)
10. Mesclagem das tabelas `employee` e `departament` para criar uma tabela `employee` com o nome dos departamentos associados aos colaboradores

    10.1 Mesclagem realizada: junção externa esquerda, onde `employee.Dno = departament.Dnumber`, seguida da eliminação das colunas desnecessárias, como `Dno` e `Dnumber`
11. Junção dos colaboradores e respectivos nomes dos gerentes (vide passo 5)
12. Mesclagem das colunas `Fname`, `Minit` e `Lname` de `employee` para formar uma coluna única com o nome completo

    12.1 Ferramenta utilizada: `Adicionar coluna > Coluna de exemplos`
13. Mesclagem das tabelas `departaments` e `dept_locations`, de maneira que cada combinação departamento-local seja única

    13.1 Mesclagem realizada: junção externa esquerda, onde `departaments.Dnumber = dept_locations.Dnumber`
14. "Explique por que, neste caso supracitado, podemos apenas utilizar o mesclar e não o atribuir."
    - No caso acima, podemos utilizar apenas o mesclar e não o atribuir (ou acrescentar), pois o atribuir funciona como o `UNION` do SQL, acrescentando os valores como novos registros (ou seja, novas linhas), enquanto o mesclar funciona como o `JOIN` do SQL, de maneira a possibilitar o acréscimo dos valores como colunas, com base na correspondência determinada.
15. Agrupamento dos dados, a fim de saber quantos colaboradores existem por gerente

    15.1 (imagem)
16. Eliminação das colunas desnecessárias.

