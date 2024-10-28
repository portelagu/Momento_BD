# Momento 

Contém a base de indicados da empresa Momento para treinar consultas complexas no MongoDB.

Vamos fazer algumas perguntas para brincar de análise exploratória de dados com MongoDB.

* Quantos funcionarios da empresa Momento trabalham no departamento de vendas?
<p>R: 5</p>
<p>Q:</p>

```sql
SELECT COUNT(*) 
FROM funcionarios 
JOIN departamentos ON funcionarios.departamento_id = departamentos.departamento_id 
WHERE departamentos.departamento_nome = 'Vendas';
```

* Inclua suas próprias informações no departamento de Tecnologia da empresa.
<p>Q:</p>

```sql
INSERT INTO funcionarios (primeiro_nome, sobrenome, email, senha, telefone, data_contratacao, cargo_id, salario, departamento_id) 
VALUES ('Gustavo', 'Gomes Portela', 'ggomesportela26@gmail.com', 'essaehumasenhaforte', '999999999', CURDATE(), 9, 5000.00, 3);
```

* Agora diga, quantos funcionários temos ao total na empresa?
<p>R: 42</p>
<p>Q:</p>

```sql
SELECT COUNT(*) FROM funcionarios;
```

* E quanto ao Departamento de Tecnologia?
<p>R: 5</p>
<p>Q:</p>

```sql
SELECT COUNT(*) 
FROM funcionarios 
JOIN departamentos ON funcionarios.departamento_id = departamentos.departamento_id 
WHERE departamentos.departamento_nome = 'Tecnologia';
```

* Quanto o departamento de Vendas gasta em salários?
<p>R: R$51500.00</p>
<p>Q:</p>

```sql
SELECT SUM(salario) 
FROM funcionarios 
JOIN departamentos ON funcionarios.departamento_id = departamentos.departamento_id 
WHERE departamentos.departamento_nome = 'Vendas';
```

* Um novo departamento foi criado. O departamento de Inovações. 
Ele será locado no Brasil. Por favor, adicione-o no banco de dados da empresa colocando quaisquer informações que você achar relevantes.
<p>Q:</p>

```sql
INSERT INTO departamentos (departamento_nome, escritorio_id)
VALUES ('Inovações', 3900);
```

* O departamento de Inovações está sem funcionários. Inclua alguns colegas de turma nesse departamento. 
<p>Q:</p>

```sql
INSERT INTO funcionarios (primeiro_nome, sobrenome, email, senha, telefone, data_contratacao, cargo_id, salario, departamento_id)
VALUES ('Josineudo', 'Arruda', 'joharruda@hotmail.com', '9999999', '11933333333', CURDATE(), 9, 4500.00, 15),
('Caroline', 'Simião', 'carolsimiao@hotmail.com', '888888', '119888888888', CURDATE(), 9, 4700.00, 15);
``` 

* Quantos funcionarios a empresa Momento tem agora?
<p>R: 44</p>
<p>Q:</p>

```sql
SELECT COUNT(*) FROM funcionarios;
```

* Quantos funcionários da empresa Momento possuem conjuges?
<p>R: 44</p>
<p>Q:</p>

```sql
SELECT COUNT(DISTINCT funcionario_id) 
FROM dependentes 
WHERE relacionamento = 'Cônjuge';
```

* Qual a média salarial dos funcionários da empresa Momento, excluindo-se o CEO?
<p>R: 8372.79</p>
<p>Q:</p>

```sql
SELECT AVG(salario) FROM funcionarios WHERE cargo_id != 4;
```

* Qual a média salarial do departamento de tecnologia?
<p>R: 5760</p>
<p>Q:</p>

```sql
SELECT AVG(salario) 
FROM funcionarios 
JOIN departamentos ON funcionarios.departamento_id = departamentos.departamento_id 
WHERE departamentos.departamento_nome = 'Tecnologia';
``` 

* Qual o departamento com a maior média salarial?
<p>R: Tecnologias Avançadas</p>
<p>Q:</p>

```sql
SELECT departamento_nome, AVG(salario) AS media_salario
FROM funcionarios JOIN departamentos ON funcionarios.departamento_id = departamentos.departamento_id 
GROUP BY departamento_nome ORDER BY media_salario DESC LIMIT 1;
```

* Qual o departamento com o menor número de funcionários?
<p>R: Administração</p>
<p>Q:</p>

```sql
SELECT departamento_nome, COUNT(funcionario_id) AS num_funcionarios
FROM funcionarios 
JOIN departamentos ON funcionarios.departamento_id = departamentos.departamento_id 
GROUP BY departamento_nome
ORDER BY num_funcionarios ASC
LIMIT 1;
```

* Pensando na relação quantidade e valor unitario, qual o produto mais valioso da empresa?
<p>R: Uniforme do Superman</p>
<p>Q:</p>

```sql
SELECT produto_nome, MAX(produto_price)
FROM produtos;
```


* Qual o produto mais vendido da empresa?
<p>R: Uniforme do Superman</p>
<p>Q:</p>

```sql
SELECT produto_nome, SUM(quantidade) AS total_vendido
FROM vendas 
JOIN produtos ON vendas.produto_id = produtos.produto_id 
GROUP BY produto_nome
ORDER BY total_vendido DESC
LIMIT 1;
```

* Qual o produto menos vendido da empresa?
<p>R: Batarangs Oficiais</p>
<p>Q:</p>

```sql
SELECT produto_nome, SUM(quantidade) AS total_vendido
FROM vendas 
JOIN produtos ON vendas.produto_id = produtos.produto_id 
GROUP BY produto_nome
ORDER BY total_vendido ASC
LIMIT 1;
```

* Qual o funcionário contratado há mais tempo na empresa?
<p>R: Steven Wayne</p>
<p>Q:</p>

```sql
SELECT primeiro_nome, sobrenome, data_contratacao 
FROM funcionarios 
ORDER BY data_contratacao ASC
LIMIT 1;
```

* Qual o funcionário contratado há menos tempo na empresa?
<p>R: Eu (Gustavo Portela)</p>
<p>Q:</p>

```sql
SELECT primeiro_nome, sobrenome, data_contratacao 
FROM funcionarios 
ORDER BY data_contratacao DESC
LIMIT 1;
```