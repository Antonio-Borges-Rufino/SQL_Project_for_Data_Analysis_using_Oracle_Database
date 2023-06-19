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
