## QUESTÃO 01

 

**> ***Prepare um relatório que mostre a média salarial dos funcionários de cada departamento*****

select avg(salario) as media_salarial, numero_departamento

from funcionario

group by numero_departamento ;



## QUESTÃO 02

**> ***Prepare um relatório que mostre a média salarial dos homens e das mulheres.*****

select avg(salario) as media, sexo

from funcionario

group by sexo;

## QUESTÃO 03


**> ***prepare um relatório que liste o nome dos departamentos e, para cada departamento, inclua as seguintes informações de seus funcionários: o nome completo, a data de nascimento, a idade em anos completos e o salário.*****


select nome_departamento,

concat(primeiro_nome, ' ', nome_meio, ' ', ultimo_nome) as nome_funcionario, data_nascimento,

extract(year from age (funcionario.data_nascimento)) as idade,salario

from departamento, funcionario

where departamento.numero_departamento = funcionario.numero_departamento;


## QUESTÃO 04


**> ***repare um relatório que mostre o nome completo dos funcionários, a idade em anos completos, o salário atual e o salário com um reajuste que obedece ao seguinte critério: se o salário atual do funcionário é inferior a 35.000 o reajuste deve ser de 20%, e se o salário atual do funcionário for igual ou superior a 35.000 o reajuste deve ser de 15%.*****

select concat(primeiro_nome, ' ', nome_meio, ' ', ultimo_nome) as nome_funcionario,

data_nascimento,

salario,

case when salario < 35000 then salario * 1.2

when salario >= 35000 then salario * 1.15

end as reajuste_salario from funcionario;


## QUESTÃO 05


**> ***Prepare um relatório que liste, para cada departamento, o nome do gerente e o nome dos funcionários. Ordene esse relatório por nome do departamento (em ordem crescente) e por salário dos funcionários (em ordem decrescente).*****



## QUESTÃO 06


**> ***sample text*****


## QUESTÃO 07


**> ***sample text*****



## QUESTÃO 08


**> ***sample text*****


## QUESTÃO 09


**> ***sample text*****


## QUESTÃO 10


**> ***sample text*****


## QUESTÃO 11


**> ***sample text*****


## QUESTÃO 12


**> ***sample text*****


## QUESTÃO 13


**> ***sample text*****

## QUESTÃO 14


**> ***sample text*****


## QUESTÃO 15


**> ***sample text*****













