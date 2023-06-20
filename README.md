# REFERENCIA
1. ESSE PROJETO ADVEM DO SITE www.projectpro.io e é uma compilação dos projetos SQL Project for Data Analysis using Oracle Database
  das partes 1 a 7

# Informações Gerais
1. Motivação  
    -> Aprender os diferentes usos do Oracle Database   
2. Diagrama de Aprendizado
![](https://github.com/Antonio-Borges-Rufino/SQL_Project_for_Data_Analysis_using_Oracle_Database/blob/main/3596zn01.png)  
3. Os dados são de responsabilidade do projectpro

# LISTA DE APRENDIZADO
1. APRENDI A MANIPULAR DADOS NO ORACLE DATABASE  
2. APRENDI A MANIPULAR DADOS FALTANTES COM DIFERENTES CASOS DE USO  
3. APRENDI COMANDOS DDL E DML NO ORACLE
4. APLIQUEI EM DIFERENTES CASOS DE USO JUNÇÕES DE TABELA, QUERY DENTRO DE QUERY E TABELAS PERSONALIZADAS
5. USEI EM DIFERENTES DATASETS E CASOS DE USO DIVERSOS TIPOS DE ORDENAÇÃO E AGRUPAMENTO
6. TRABALHEI COM DADOS DO TIPO BLOB

# CASOS DE USO
1. DETALHES DA CAIXA POSTAL 98199 
```
SELECT * 
FROM LOCATIONS
WHERE POSTAL_CODE = '98199';
```
2. INFORMAÇÕES SOBRE ID DE LOCAÇÃO
```
SELECT *
FROM departments
WHERE LOCATION_ID = '1700';
```
3. MOSTRAR TODOS OS DEPARTAMENTOS
```
SELECT department_name
FROM departments
WHERE LOCATION_ID = '1700';
```
4. VISUALIZAR SALARIOS MAIORES QUE 10000
```
SELECT *
FROM employees
where salary >= '10000';
```
5. VER APENAS NOME, EMAIL E NUMERO DE TELEFONE 
```
SELECT first_name,email,phone_number
FROM employees
WHERE salary > '10000';
```
6. ENCONTRAR O FUNCIONARIO DO DEPARTAMENTO DE MARKETING COM SALARIO MENOR OU IGUAL A 10000 
```
-- O DEPARTAMENTO DE MARKETING É DEPARTAMENT_ID = 20 --
SELECT *
FROM employees
WHERE department_id = 20 and salary < 10000;
```
7. PESQUISAR REGISTROS NAO NULOS 
```
SELECT *
FROM employees
WHERE commission_pct IS NOT NULL;
```
8. PESQUISAR OS FUNCIONARIOS QUE NAO TEM GERENTE
```
SELECT *
FROM employees
WHERE manager_id IS NULL;
```
9. PESQUISAR OS NOMES DOS FUNCIONARIOS EM ORDEM 
```
SELECT FIRST_NAME ||' ' || LAST_NAME
FROM employees
ORDER BY FIRST_NAME,LAST_NAME
```
10. PESQUISAR TODOS OS REGISTROS DO CODIGO POSTAL UK
```
SELECT *
FROM locations
WHERE country_id = 'UK'
ORDER BY city;
```
11. PESQUISAR TODOS OS REGISTROS DO CODIGO POSTAL UK DESC
```
SELECT *
FROM locations
WHERE country_id = 'UK'
ORDER BY city DESC;
```
12. DPESQUISAR REGISTROS NULOS POR PRIMEIRO
```
SELECT *
FROM locations
WHERE country_id = 'UK'
ORDER BY city NULLs FIRST;
```
13. MODIFICAR PARA ORDENAR EM MAIS DE UMA POSIÇÃO 
```
SELECT *
FROM locations
ORDER BY country_id asc,city DESC;
```
14. PESQUISAR CARGOS DE TRABALHO ESPECIFICOS USANDO IN
```
SELECT *
FROM jobs
WHERE job_title in ('President','Finance Manager','Programmer');
```

 15. PESQUISAR CARGOS DE TRABALHO ESPECIFICOS QUE NÃO DO GRUPO SELECIONADO 
```
SELECT *
FROM jobs
WHERE job_title not in ('President','Finance Manager','Programmer');
```
16. USO DE CARACTER CORINGA USANDO LIKE
```
SELECT *
FROM employees
WHERE job_id LIKE 'AD%';
```
17. OUTRAS POSSIBILIDADES DE USO DE CARACTER CORINGA, DE FORMA MAIS ABRANGENTE
```
SELECT *
FROM employees
WHERE first_name LIKE 'A%'
AND first_name NOT LIKE '%a'
```
18. COMANDO INSERT SEM USO DE SELECT
```
INSERT INTO employees (employee_id,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID)
VALUES 
    (207
    , 'Antonio'
    , 'Rufino'
    , 'xxx@gmail.com'
    , '111.111.1111'
    , TO_DATE('10-06-2023','dd-mm-yyyy')
    , 'HR_REP'
    , 10000
    , NULL
    , 205
    , 20
    );
```
19. COMANDO UPDATE 
```
update employees
SET salary = 100000
WHERE employee_id = 207;
```
20. COMANDO DELET
```
delete employees
where employee_id = 207;
```
21. TRABALHANDO O COMANDO DE ROLLBACK 
```
SELECT * 
FROM employees
order by employee_id desc;

rollback;

INSERT INTO employees (employee_id,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID)
VALUES 
    (207
    , 'Antonio'
    , 'Rufino'
    , 'xxx@gmail.com'
    , '111.111.1111'
    , TO_DATE('10-06-2023','dd-mm-yyyy')
    , 'HR_REP'
    , 10000
    , NULL
    , 205
    , 20
    );
-- PARA VOLTAR ANTES DA INSERÇÃO DO REGISTRO, BASTA EXECUTAR O ROLLBACK DE NOVO
```
22. CRIAR UM BACKUP DE UMA TABELA USANDO O COMANDO INSERT COM SELECT
```
CREATE TABLE employees_baclup AS (SELECT * FROM employees)
SELECT * FROM employees_baclup
```
23. USANDO O ROLBACK E O COMMIT PARA PERSISTENCIA
```
rollback;
-- APAGAR TODOS OS REGISTROS DE UMA TABELA --
TRUNCATE TABLE employees_baclup
-- INSERIR DE NOVO TODOS OS REGISTROS NA TABELA --
INSERT INTO employees_baclup SELECT * FROM employees
commit; -- O COMITE SERVE PARA EVITAR UM ROLBACK E A PERDA DA INFORMAÇÃO 
```
24. USANDO O DISTINCT PARA VISUALIZAR VALORES UNICOS
```
SELECT DISTINCT country_id
FROM locations
ORDER BY country_id;
```
25. USO DE UM SELECT DENTRO DE UMA CLAUSULA IN PARA AUMENTAR O FILTRO
```
-- BUSCANDO O NOME DOS GERENTES --
SELECT first_name ||' '|| last_name as NAME FROM employees 
WHERE EMPLOYEE_ID IN (Select distinct manager_id from departments);
```
26. USO DE CONDIÇÕES ANINHADAS
```
-- job_id = AD%  e salary < 15000 --
-- OR job_id = S% e salaray > 10000 -- 
SELECT * 
FROM EMPLOYEES
WHERE (
(job_id LIKE 'AD%' and salary > 15000) 
or (job_id LIKE 'S%' and salary < 10000)
);
```
27. JUNTANDO TABELAS SEM O USO DO JOIN
```
SELECT *
FROM employees, departments
where employees.department_id = departments.department_id
and departments.department_name = 'Marketing'
```
28. FAZENDO A JUNÇÃO DE TABELAS USANDO O JOIN
```
SELECT * 
FROM employees INNER JOIN departments 
ON employees.department_id = departments.department_id 
AND departments.department_name = 'Marketing'
INNER JOIN locations
ON departments.LOCATION_ID = locations.LOCATION_ID;
```
29. EM ALGUNS CASO, EXISTE A NECESSIDADE DO USO DO LEFT JOIN
```
SELECT * 
FROM departments LEFT OUTER JOIN employees 
ON departments.department_id = employees.department_id
ORDER BY departments.MANAGER_ID NULLS FIRST;
```
30. O RIGHT JOIN É A MESMA COISA DO LEFT, MAS AO CONTRARIO, COM A LEITURA COMEÇANDO DA DIREITA PARA ESQUERDA
```
SELECT * 
FROM departments RIGHT OUTER JOIN employees
ON departments.DEPARTMENT_ID = employees.DEPARTMENT_ID
ORDER BY departments.DEPARTMENT_ID;
```
31. USANDO O FULL JOIN
```
SELECT * 
from departments FULL OUTER JOIN employees
ON departments.DEPARTMENT_ID = employees.DEPARTMENT_ID
ORDER BY departments.DEPARTMENT_ID;
```

32. USANDO JOIN EM CONSULTAS COM A MESMA TABELA, MOSTRANDO UM CASO DE USO ESPECIAL
```
SELECT a.FIRST_NAME ||' '|| a.LAST_NAME AS FUNCIONARIO,
a.EMPLOYEE_ID, b.FIRST_NAME ||' '|| b.LAST_NAME AS GERENTE
FROM EMPLOYEES a, employees b
WHERE a.employee_id = b.manager_id
ORDER BY FUNCIONARIO;

-- REALIZANDO A CONSULTA ANTERIOR USANDO JOIN --
SELECT a.FIRST_NAME ||' '|| a.LAST_NAME AS FUNCIONARIO,
a.EMPLOYEE_ID, b.FIRST_NAME ||' '|| b.LAST_NAME AS GERENTE
FROM EMPLOYEES a JOIN employees b
ON a.employee_id = b.manager_id
ORDER BY FUNCIONARIO;
```
33. USO DE OPERADORES DE CONJUNTOS
```
-- TRABALHANDO COM O OPERADOR UNION --
SELECT 'FUNCTIONAL' AS TYPE, CITY FROM LOCATIONS
UNION
SELECT 'N_FUNCTINAL' AS TYPE, CITY FROM LOCATIONS;

-- TRABALHANDO COM OPERADOR MINUS --
SELECT 'FUNCTIONAL' ||' '|| CITY  FROM LOCATIONS
MINUS
SELECT 'N_FUNCTINAL' ||' '|| CITY FROM LOCATIONS;

-- TRABALHANDO COM OPERADOR INTERSECT --
SELECT 'FUNCTIONAL' ||' '|| CITY  FROM LOCATIONS
INTERSECT
SELECT 'N_FUNCTINAL' ||' '|| CITY FROM LOCATIONS;
```
34. CONSTRUINDO UM SELECT COMPLETO
```
-- CRIAR UM SELECT CUSTOMIZADO -- 
SELECT 
E.first_name ||' '|| E.last_name AS NAME,
E.email,E.salary,
J.job_title, 
EE.first_name ||' '|| EE.last_name AS MANAGER,
D.department_name,
L.city,
CC.country_name
FROM employees E
LEFT OUTER JOIN JOBS J
ON E.job_id = J.job_id
LEFT OUTER JOIN employees EE
ON E.manager_id = EE.employee_id
LEFT OUTER JOIN departments D
ON E.department_id = D.department_id
LEFT OUTER JOIN locations L
ON D.location_id = L.location_id
LEFT OUTER JOIN countries CC
ON CC.country_id = L.country_id
```
35. MAIS 2 CASOS DE USO DE AFUNILAMENTO DENTRO DA CLAUSULA IN USANDO SELECT
```
-- USO 1 --
SELECT first_name ||' '|| last_name as NAME FROM employees 
WHERE EMPLOYEE_ID IN (Select distinct manager_id from departments);

-- USO 2 --
SELECT d.department_name FROM departments d
WHERE d.department_id IN 
(SELECT e.department_id FROM employees e WHERE e.salary > 10000)
```

36. USO DA FUNÇÃO DE AGREGAÇÃO MAX
```
SELECT * FROM employees 
WHERE salary IN (SELECT MAX(salary) FROM employees);
```
37. USO DA FUNÇÃO DE AGREGAÇÃO MIN
```
SELECT * FROM employees 
WHERE salary IN (SELECT MIN(salary) FROM employees);
```
38. USO DA FUNÇÃO DE SUMARAZIÇÃO 
```
SELECT SUM(salary) FROM EMPLOYEES;
```
39. USO DA FUNÇÃO COUNT 
```
SELECT COUNT(*) FROM EMPLOYEES;
```
40. USO DA FUNÇÃO DE MÉDIA UTILIZANDO O ARREDONDAMENTO ROUND
```
SELECT ROUND(AVG(SALARY),2) FROM EMPLOYEES;
```
41. USO EM UM SELECT DAS FUNÇÕES DE AGREGAÇÃO, SEM A NECESSIDADE DE UTLIZAR AGRUPAMENTOS
```
-- ENCONTRAR TODOS OS FUNCIONARIOS DE TI --
-- ADIMITIDOS DEPOIS DE 01/01/98 --
-- E QUE POSSUEM SALARIO MAIOR QUE A MEDIA --
SELECT e.first_name,e.department_id FROM employees e 
WHERE e.department_id IN (SELECT department_id FROM departments 
WHERE department_name LIKE 'IT%') AND
e.hire_date > TO_DATE('01-01-1998','dd-mm-yyyy') AND
e.salary > (SELECT AVG(salary)FROM employees)
```
42. E CONVENIENTE USAR ALGUMAS FUNÇÕES DE AGREGAÇÃO UTILIZANDO O GROUP BY (AGRUPAMENTO)
```
SELECT d.department_name,
COUNT(*) AS "QTD",
ROUND(AVG(e.salary),2)
FROM departments d
JOIN employees e
ON e.department_id = d.department_id
GROUP BY d.department_name
ORDER BY "QTD";

-- USO 2 --
SELECT em.first_name, 
COUNT(e.employee_id) AS "MANAGER_EMPLOYEED" 
FROM employees e
JOIN employees em
ON e.manager_id = em.employee_id 
GROUP BY em.first_name
ORDER BY "MANAGER_EMPLOYEED"  DESC;
```

43. USO DO AGRUPAMENTO UTILZANDO A CLAUSULA HEAVING, ELA SE DIFERE DO WHERE POIS ACONTECE DIRETAMENTE PARA O AGRUPAMENTO
```
SELECT DEPARTMENTS.DEPARTMENT_NAME,
MAX(SALARY) AS "MAX_SALARY"
FROM EMPLOYEES
JOIN DEPARTMENTS
ON EMPLOYEES.DEPARTMENT_ID     = DEPARTMENTS.DEPARTMENT_ID
WHERE EMPLOYEES.DEPARTMENT_ID IS NOT NULL
GROUP BY DEPARTMENTS.DEPARTMENT_NAME
HAVING MAX(SALARY) > 10000
ORDER BY MAX_SALARY ASC,
DEPARTMENT_NAME DESC;
```

44. QUANDO VOCE TEM POUCAS LINHAS, É MAIS CONVENIENTE USAR A CLAUSULA EXIST, DO QUE A IN 
```
SELECT * 
FROM DEPARTMENTS
WHERE EXISTS (SELECT * FROM EMPLOYEES WHERE EMPLOYEES.DEPARTMENT_ID = DEPARTMENTS.DEPARTMENT_ID);
```
45. PODEMOS CATEGORIZAR OS DADOS FACILITANDO O ENTENDIMENTO 
```
SELECT e.first_name||' '||e.last_name,
e.hire_date,
CASE
    WHEN e.hire_date < TO_DATE('01-JAN-1990','dd-MON-yyyy') THEN 'ANTES_90'
    WHEN (e.hire_date > TO_DATE('01-JAN-1990','dd-MON-yyyy') and (e.hire_date < TO_DATE('01-JAN-1995','dd-MON-yyyy'))) THEN 'ENTRE_90-95'
    ELSE
        'DEPOIS_95'
END
FROM employees e;
```
46. A CLALSULA WITH PERMITE CONSTRUIR UMA "TABELA TEMPORARIA" PARA QUE POSSAMOS USAR NO SELECT, ISSO E BASTANTE UTIL PRA REDUZIR A DIMENSÃO DO SELECT
```
-- DESCOBRIR QUAL DEPARTAMENTO TEM A MÉDIA SALARIAL MAIOR QUE A MEDIA TOTAL --
WITH MEDIA_DEPARTAMENTO AS
(SELECT e.department_id, ROUND(AVG(e.salary),2) AS "MEDIA_DEP" FROM employees e GROUP BY e.department_id),
MEDIA_TOTAL AS (SELECT ROUND(AVG(e.salary),2) AS "MEDIA_T" FROM employees e)
SELECT * FROM MEDIA_DEPARTAMENTO, MEDIA_TOTAL
WHERE MEDIA_DEPARTAMENTO.MEDIA_DEP > MEDIA_TOTAL.MEDIA_T;
```
47. OUTRA OPÇÃO É CRIAR TABELA VIEWR
```
CREATE OR REPLACE VIEW FUNCIONARIOS_BEM_PAGOS AS
WITH MEDIA_TOTAL AS (SELECT ROUND(AVG(salary),2) AS "MEDIA_TOTAL_SAL" FROM employees)
SELECT e.first_name||' '||e.last_name AS "NOME",e.salary,e.department_id FROM employees e, MEDIA_TOTAL
WHERE e.salary > MEDIA_TOTAL.MEDIA_TOTAL_SAL;

SELECT * FROM FUNCIONARIOS_BEM_PAGOS
```
48. ROWRUM PERMITE UMA ESPÉCIE DE INDEXAÇÃO, NÃO INDEXA DE FATO, MAS ELA ENUMERA AS LINHAS, ISSO É ESPECIALMENTE IMPORTANTE QUANDO NÃO TEMOS PK
```
SELECT * FROM EMPLOYEES 
WHERE salary NOT IN 
(SELECT * FROM 
(SELECT e.salary FROM employees e GROUP BY e.salary ORDER BY e.salary DESC) 
WHERE ROWNUM < 3);
```
49. A FUNÇÃO LISTAGG PERMITE APRESENTAR INFORMAÇÕES EM FORMA DE LISTA
```
SELECT DISTINCT LISTAGG(e.city,',') WITHIN GROUP(ORDER BY e.city)AS CITY
FROM locations e;

-- CRIANDO LISTA SEPARADA POR VIRGULAS --
SELECT e.country_id,LISTAGG(e.city,',') WITHIN GROUP(ORDER BY e.city)AS CITY
FROM locations e
GROUP BY e.country_id;
```
50. ROWNUM DEFINE COMO SEQUENCIAL UM SELECT NORMAL, QUANDO ALTERAMOS A ORDEM UTILIZANDO ORDER BY OU FAZENDO ALGUMA CLAUSULA WHERE ELE NÃO FUNCIONA, MOSTRANDO A ORDEM DO SELECT NORMAL. PARA SUPERAR ESSE PROBLEMA, UTILIZA-SE ROW_NUMBER()
```
-- COMO NO EXEMPLO ABAIXO, ONDE ROWNUM NÃO DEFINIU SEQUENCIALMENTE --
SELECT ROWNUM,e.* FROM EMPLOYEES e
ORDER BY e.salary;
-- PARA ISSO, USA-SE UMA FUNÇÃO ESPECIFICA CHAMADA ROW_NUMBER OVER() --
SELECT ROW_NUMBER() OVER (ORDER BY e.salary) AS "ORD", e.* FROM EMPLOYEES e
```
51. EM ALGUNS CASOS, TEMOS QUE DIFERENCIAR LINHAS IGUAIS, ISSO OCORRE QUANDO NÃO SE TEM CHAVE PRIMÁRIA E UM REGISTRO É REPETIDO, AS VEZES ATÉ MESMO COM ALGUMA INFORMAÇÃO CONFLITANTE, COM ISSO, PODEMOS USAR ROW_NUMBER() OVER() COM PARTICIONAMENTO, O PARTCIONAMENTO É UMA CLAUSULA QUE SEPARA DADOS DE UMA MESMA CLASSE, OU SEJA, É COMO SE FOSSE UM ORDER BY PARA DADOS. NO EXEMPLO ABAIXO PARTICIONAMOS OS DADOS ONDE ELES ESTAVAM SE REPETINDO
```
SELECT e.employee_id||'.'||ROW_NUMBER() OVER (PARTITION BY e.employee_id ORDER BY e.commission_pct) "RNK",
e.*
FROM employees e;
```
52. PODE-SE USAR O PARTICIONAMENTO DE OUTRAS FORMAS TAMBEM, COMO POR EXEMPLO, PARA CLASSIFICAR OS SALARIOS DENTRO DE UM MESMO GRUPO DE TRABALHO
```
SELECT e.employee_id||'.'||ROW_NUMBER() OVER (PARTITION BY e.job_id ORDER BY e.salary) "RNK",
e.*
FROM employees e
ORDER BY e.job_id;
```
53. ENTRETANTO, ESSA SITUAÇÃO PODE DECORRER EM ERROS, POR EXEMPLO, SE UM SALÁRIO RANKEADO COMO 2 FOR IGUAL A OUTROS 3 SALARIOS, OS OUTROS 3 SALARIOS OCUPARIAM AS POSIÇÕES 3,4,5, EM VEZ DE OCUPAR TODOS AS POSIÇÕES 2, PARA RESOLVER ISSO USA-SE RANK
```
SELECT e.employee_id||'.'||ROW_NUMBER() OVER (PARTITION BY e.job_id ORDER BY e.salary) "RNK",
RANK() OVER (PARTITION BY e.job_id ORDER BY e.salary) "RANK_CERTO",e.*
FROM employees e
ORDER BY e.job_id;
```
54. O PROBLEMA DE RANK() É QUE QUANDO SE TEM POSIÇÕES REPETIDAS, COMO 4 PESSOAS NA POSIÇÃO 2, A PRIMEIRA LINHA APÓS A POSIÇÃO 2 EM VEZ DE SER RANKEADA COMO 3, É RANKEADA COMO 7, PARA LIDAR COM ISSO USA-SE DENSE_RANK()
```
SELECT e.employee_id||'.'||ROW_NUMBER() OVER (PARTITION BY e.job_id ORDER BY e.salary) "RNK",
RANK() OVER (PARTITION BY e.job_id ORDER BY e.salary) "RANK_EMPATE",
DENSE_RANK() OVER (PARTITION BY e.job_id ORDER BY e.salary) "RANK_CONTINUO"
,e.*
FROM employees e
ORDER BY e.job_id;
```
55. AS VEZES EXISTE A NECESSIDADE DE TRABALHAR AS STRINGS, POR EXEMPLO, QUANDO TEMOS UM TEXTO MUITO GRANDE E QUEREMOS APENAS PARTE DAQUELA INFORMAÇÃO, USA-SE A FUNÇÃO SUBSTR, QUE RETORNA APENAS UMA PARTE DA STRING
```
SELECT e.phone_number, SUBSTR(e.phone_number,8) FROM employees e;
-- RETORNANDO APENAS UM PEDAÇO DO RETORNO
SELECT e.phone_number, SUBSTR(e.phone_number,8,2) FROM employees e;
```
56. CASO EXISTA A NECESSIDADE DE UMA OCORRENCIA EM ESPECIFICO, COMO A POSIÇÃO DE UM "." NO TEXTO OU ALGO PARECIDO, USA-SE INSTR
```
SELECT e.phone_number, INSTR(e.phone_number,'.',-1) FROM employees e;
```
57. PODEMOS MISTURAR AS 2 CLAUSULAS PARA PODER FAZER PROCESSAMENTOS MAIS INTERESSANTES
```
-- MISTURANDO AS 2 CLAUSULAS 
-- A MISTURA GARANTE QUE NUMEROS QUE TENHAM QUANTIDADES DIFERENTES FIQUEM NA MESMA FORMATAÇÃO
SELECT e.phone_number, SUBSTR(e.phone_number,INSTR(e.phone_number,'.',-1)) FROM employees e;
```
58. AS FUNÇÕES DE TEXTOS POSSUEM UMA INFIDADE DE USOS, E TAMBÉM UMA LONGA LISTA, ABAIXO ESTÁ UMA LONGA LISTA DE FUNÇÕES QUE PODEMOS USAR PARA FORMATAR TEXTOS
```
-- FUNÇÕES INTERESSANTES
-- FUNÇÃO DE CONCATENAÇÃO
SELECT CONCAT(e.first_name,CONCAT(' ',e.last_name)) FROM employees e;
-- FUNÇÃO DE DEIXAR TUDO MAIUSCULO
SELECT UPPER(e.first_name) FROM employees e;
-- FUNÇÃO DE DEIXAR TUDO MINUSCULO
SELECT LOWER(e.first_name) FROM employees e;
-- PRIMEIRA LETRA MAISCULA
SELECT INITCAP(e.first_name) FROM employees e;
-- REMOVER ESPAÇO A DIREITA
SELECT RTRIM(e.first_name) FROM employees e;
-- REMOVER ESPAÇO A ESQUERDA
SELECT LTRIM(e.first_name) FROM employees e;
-- REMOVA AMBOS AO MESMO TEMPO
SELECT TRIM(e.first_name) FROM employees e;
-- FORMATAR TAMANHO DA ESQUERDA PRA DIREITA PREENCHENDO ESPAÇOS VAZIOS
SELECT DISTINCT e.commission_pct, LPAD(e.commission_pct,5,0) FROM employees e;
-- FORMATAR TAMANHO DA DIREITA PRA ESQUERDA PREENCHENDO ESPAÇOS VAZIOS
SELECT DISTINCT e.commission_pct, RPAD(e.commission_pct,5,0) FROM employees e;
-- VER O TAMANHO DE UM REGISTRO
SELECT e.first_name,LENGTH(e.first_name) FROM employees e;
```
59. AS VEZES ALGUMAS COLUNAS PODEM TER VALORES NULOS, E É NECESSÁRIO TRABALHAR COM ELES, COALESCE TRABALHA COMO SE FOSSE UMA ESPÉCIE DE SE SENÃO PARA VALORES NULOS
```
-- O PRIMEIRO ARGUMENTO É O RETORNO CASO SEJA NAO NULO, O SEGUNDO E O RETORNO CASO SEJA NULO
SELECT e.first_name, e.salary, e.commission_pct, COALESCE(e.salary*e.commission_pct,e.salary*0.1) 
FROM employees e;
```
60. CASO EXISTA A NECESSIDADE DE MUDAR OS VALORES NULOS, USA-SE NVL
```
SELECT e.first_name, e.salary, e.commission_pct, NVL(e.commission_pct,0.1) 
FROM employees e;
```
61. ABAIXO ESTÁ UMA FORMA DE USO QUE DEMOSTRA COMO USAR PARTITION, ROW_NUMBER EM CASOS DE USOS DIFERENTES
```
-- REMOVENDO ARQUIVOS DUPLICADOS
WITH TABLE_RANK_ANIMAL AS (
SELECT ROW_NUMBER() OVER(PARTITION BY ab.id ORDER BY ab.id) AS "RANK_ID_TABLE",ab.* 
FROM animal_bites ab)
SELECT * FROM TABLE_RANK_ANIMAL
WHERE "RANK_ID_TABLE" >1;

-- CRIANDO TABELA SEM REGISTROS DUPLICADOS
CREATE TABLE ANIMAL_BITES_UNIQUE AS
SELECT ID, BITE_DATE, SPECIESIDDESC, BREEDIDDESC, 
BREED, GENDERIDDESC, COLOR, VACCINATION_YRS, 
VACCINATION_DATE, VICTIM_ZIP, ADVISSUEDYNDESC, WHEREBITTENIDDESC, 
HEAD_SENT_DATE, RELEASE_DATE, RESULTSIDDESC, FOLLOWUPYNDESC FROM (
SELECT ROW_NUMBER() OVER(PARTITION BY ab.id ORDER BY ab.id) AS "RANK_ID_TABLE",ab.* 
FROM animal_bites ab) ct
WHERE ct.RANK_ID_TABLE > 1
```
62. EM ALGUNS CASOS, AS LINHAS QUE POSSUEM VALORES NULOS NÃO PODEM FICAR NO DS, ISSO OCORRE QUANDO SÃO DE FATO EXESSENCIAIS, EXISTE DIVERSAS FORMAS DE RETIRAR VALORES NULOS, COMO DELETE E ETC, AQUI EU SO FIZ UMA TABELA SEM VALORES NULOS
```
CREATE TABLE ANIMAL_BITES_UNN AS
SELECT * FROM ANIMAL_BITES_UNIQUE
WHERE id NOT IN(
SELECT ID FROM ANIMAL_BITES_UNIQUE
WHERE bite_date IS NULL 
or speciesiddesc IS NULL 
or victim_zip IS NULL)
```
63. AS VEZES PRECISAMOS TRANSFORMAR AS COLUNAS E APRESENTALAS EM FORMATO DE LINHA, POR EXEMPLO, FAZEMOS UM DISTINCT QUE NOS RETORNA O ID DO DEPARTAMENTO E A QUANTIDADE DE FUNCIONARIOS DELE, PODEMOS EM VEZ DE APRESENTAR DE FORMA COLUNAR, APRESENTAR EM FORMA DE LINHA, COMO UMA PLANILHA DO EXCEL, PARA FAZER ISSO, USA-SE A FUNÇÃO PIVOT
```
-- EXEMPLO DE QUERY QUE PODE VIRAR PIVOT
SELECT EMPLOYEES.job_id, SUM(EMPLOYEES.salary) 
FROM EMPLOYEES
GROUP BY EMPLOYEES.job_id;

-- PERCEB-SE QUE PODEMOS TRANSFORMAR NISSO EM PIVOT, OU SEJA, "CRIANDO OUTRA TABELA" PARA ESSAS INFORMAÇÕES

SELECT *
FROM (SELECT JOB_ID, SALARY FROM EMPLOYEES)
PIVOT
(
    --<FUNCAO DE AGREG> FOR <TABELA) IN <CONDICAO>
    SUM(SALARY) FOR JOB_ID IN ('AD_PRES','AD_VP','IT_PROG')
);
```
64. A FORMATAÇÃO UNPIVOT TAMBÉM PODE SER FEITA, ELA FAZ EXATAMENTE O CONTRARIO DA OUTRA
```
-- A FORMATAÇÃO CONTRARIA TAMBEM PODE SER USADA
-- ESSA FORMATAÇÃO REQUER LETRAS MAIUSCULAS
-- CASO TENHA ALGUM TIPO DE DADO NAO STRING, CONVERTA PARA STRING
SELECT * FROM (
SELECT EMPLOYEE_ID,FIRST_NAME,LAST_NAME FROM EMPLOYEES
)
UNPIVOT
(
    NAME FOR VAL IN ("FIRST_NAME","LAST_NAME")
)
```



