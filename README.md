Repositório com os arquivos originais de julianazanelatto/Módulo 3/Desafio de Projeto

Alterações:
Derrubada a constraint fk_employee
ALTER TABLE employee DROP CONSTRAINT fk_employee;

Consultas:

Verificar o total de horas por projeto
SELECT Pno, SUM(Hours) AS TotalHoras
FROM works_on
GROUP BY Pno;

Mesclar consultas employee e departament para criar uma tabela employee com o nome dos departamentos associados aos colaboradores. A mescla terá como base a tabela employee.
SELECT e.*, d.Dname as DepName
FROM employee e
JOIN departament d ON e.Dno = d.Dnumber;

Realize a junção dos colaboradores e respectivos nomes dos gerentes.
ALTER TABLE employee
ADD COLUMN Manager VARCHAR(255);

UPDATE employee e
LEFT JOIN employee m ON e.Super_ssn = m.Ssn
SET e.Manager = CASE
                    WHEN m.Ssn IS NULL THEN 'head'
                    ELSE CONCAT(m.Fname, ' ', m.Lname)
                END;
Mescle as colunas de Nome e Sobrenome para ter apenas uma coluna definindo os nomes dos colaboradores
SELECT CONCAT(Fname, ' ', Lname) AS FullName
FROM employee;

Mescle os nomes de departamentos e localização.
SELECT d.*, dl.Dlocation as Location
FROM departament d
JOIN dept_locations dl ON d.Dnumber = dl.Dnumber;

Explique por que, neste caso supracitado, podemos apenas utilizar o mesclar e não o atribuir.
Porque assim teremos apenas os resultados com correspondência direta entre departamentos e localização, evitando assim  inconsistências que poderiam ocorrer se tentássemos simplesmente atribuir diretamente os valores da tabela dept_locations à tabela department.
