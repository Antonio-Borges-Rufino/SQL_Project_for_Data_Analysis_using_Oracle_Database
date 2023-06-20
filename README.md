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
