### Este trabalho foi realizado com a ajuda de dois colegas de turma!
#### Gabriel Negreiros Piffer
#### Guilherme Henrique Vieira



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


**> ***Prepare um relatório que liste o nome dos departamentos e, para cada departamento, inclua as seguintes informações de seus funcionários: o nome completo, a data de nascimento, a idade em anos completos e o salário.*****


select nome_departamento,

concat(primeiro_nome, ' ', nome_meio, ' ', ultimo_nome) as nome_funcionario, data_nascimento,

extract(year from age (funcionario.data_nascimento)) as idade,salario

from departamento, funcionario

where departamento.numero_departamento = funcionario.numero_departamento;


## QUESTÃO 04


**> ***Prepare um relatório que mostre o nome completo dos funcionários, a idade em anos completos, o salário atual e o salário com um reajuste que obedece ao seguinte critério: se o salário atual do funcionário é inferior a 35.000 o reajuste deve ser de 20%, e se o salário atual do funcionário for igual ou superior a 35.000 o reajuste deve ser de 15%.*****

select concat(primeiro_nome, ' ', nome_meio, ' ', ultimo_nome) as nome_funcionario,

data_nascimento,

salario,

case when salario < 35000 then salario * 1.2

when salario >= 35000 then salario * 1.15

end as reajuste_salario from funcionario;


## QUESTÃO 05


**> ***Prepare um relatório que liste, para cada departamento, o nome do gerente e o nome dos funcionários. Ordene esse relatório por nome do departamento (em ordem crescente) e por salário dos funcionários (em ordem decrescente).*****

select nome_departamento,

concat(primeiro_nome, ' ', nome_meio, ' ', ultimo_nome) as nome,

case when cpf = cpf_gerente then 'Gerente'

else 'Funcionario'

end as cargo,

salario

from departamento, funcionario

where departamento.numero_departamento = funcionario.numero_departamento

order by nome_departamento, salario desc;



## QUESTÃO 06


**> ***Prepare um relatório que mostre o nome completo dos funcionários que têm dependentes, o departamento onde eles trabalham e, para cada funcionário, também liste o nome completo dos dependentes, a idade em anos de cada dependente e o sexo (o sexo NÃO DEVE aparecer como M ou F, deve aparecer como “Masculino” ou “Feminino”).*****

select concat(funcionario.primeiro_nome,' ', funcionario.nome_meio,' ', funcionario.ultimo_nome) Funcionário, departamento.nome_departamento Departamento,

concat(d.nome_dependente,' ', funcionario.nome_meio,' ', funcionario.ultimo_nome) Dependente, extract(year from age (funcionario.data_nascimento)) as idade,

case

when d.sexo = 'F' then 'Feminino'

when d.sexo = 'M' then 'Masculino'

end "sexo_dependente"

from funcionario

inner join departamento

on funcionario.numero_departamento = departamento.numero_departamento

inner join dependente d

on funcionario.cpf = d.cpf_funcionario;


## QUESTÃO 07


**> ***Prepare um relatório que mostre, para cada funcionário que NÃO TEM dependente, seu nome completo, departamento e salário*****

select concat (primeiro_nome, ' ', nome_meio, ' ', ultimo_nome) as nome_completo,nome_departamento,salario

from departamento, funcionario

left join dependente

on funcionario.cpf = dependente.cpf_funcionario

where dependente.cpf_funcionario is null

and funcionario.numero_departamento = departamento.numero_departamento

order by nome_departamento, salario desc



## QUESTÃO 08


**> ***Prepare um relatório que mostre, para cada departamento, os projetos desse departamento e o nome completo dos funcionários que estão alocados em cada projeto. Além disso inclua o número de horas trabalhadas por cada funcionário, em cada projeto*****

select concat (f.primeiro_nome,' ', f.nome_meio,' ',f.ultimo_nome) as nomeCompleto_funcionario, d.nome_departamento, p.nome_projeto, t.horas

from funcionario f

inner join departamento d on d.numero_departamento = f.numero_departamento

inner join trabalha_em t on t.cpf_funcionario = f.CPF

inner join projeto p on p.numero_projeto = t.numero_projeto

order by p.numero_projeto


## QUESTÃO 09


**> ***Prepare um relatório que mostre a soma total das horas de cada projeto em cada departamento. Obs.: o relatório deve exibir o nome do departamento, o nome do projeto e a soma total das horas.*****

select nome_departamento,nome_projeto,

sum(horas) as total_horas

from elmasri.departamento dp

inner join elmasri.projeto p on (dp.numero_departamento = p.numero_departamento)

inner join elmasri.trabalha_em t on (p.numero_projeto = t.numero_projeto)

group by nome_departamento, nome_projeto;


## QUESTÃO 10

*PERGUNTA REPETIDA*

**> ***~~prepare um relatório que mostre a média salarial dos funcionários de cada departamento.~~*****


## QUESTÃO 11


**> ***considerando que o valor pago por hora trabalhada em um projeto é de 50 reais, prepare um relatório que mostre o nome completo do funcionário, o nome do projeto e o valor total que o funcionário receberá referente às horas trabalhadas naquele projeto.*****

select distinct

concat(primeiro_nome,' ', nome_meio,' ', ultimo_nome) AS nome_completo_funcionario,nome_projeto,

sum(horas * 50) as valor_total

from elmasri.funcionario f

inner join elmasri.projeto p on (f.numero_departamento = p.numero_departamento)

inner join elmasri.trabalha_em t on (p.numero_projeto = t.numero_projeto)

group by nome_completo_funcionario, nome_projeto

order by nome_completo_funcionario;


## QUESTÃO 12


**> ***Seu chefe está verificando as horas trabalhadas pelos funcionários nos projetos e percebeu que alguns funcionários, mesmo estando alocadas à algum projeto, não registraram nenhuma hora trabalhada. Sua tarefa é preparar um relatório que liste o nome do departamento, o nome do projeto e o nome dos funcionários que, mesmo estando alocados a algum projeto, não registraram nenhuma hora trabalhada*****

select nome_departamento,nome_projeto,primeiro_nome as nome_funcionario

from elmasri.projeto p

inner join elmasri.departamento dp on (p.numero_departamento = dp.numero_departamento)

inner join elmasri.funcionario f on (p.numero_departamento = f.numero_departamento)

inner join elmasri.trabalha_em t on (p.numero_projeto = t.numero_projeto)

where t.horas is null or t.horas = 0;


## QUESTÃO 13


**> ***Durante o natal deste ano a empresa irá presentear todos os funcionários e todos os dependentes (sim, a empresa vai dar um presente para cada funcionário e um presente para cada dependente de cada funcionário) e pediu para que você preparasse um relatório que listasse o nome completo das pessoas a serem presenteadas (funcionários e dependentes), o sexo e a idade em anos completos (para poder comprar um presente adequado). Esse relatório deve estar ordenado pela idade em anos completos, de forma decrescente.*****

select

concat (primeiro_nome,' ', nome_meio,' ', ultimo_nome)as nome_completo_pessoa,sexo as sexo,

date_part('year', CURRENT_DATE) - DATE_PART('year', data_nascimento) as idade

from elmasri.funcionario

union

select concat(nome_dependente, ' ', f.ultimo_nome),d.sexo,

date_part('year', CURRENT_DATE) - DATE_PART('year', d.data_nascimento)

from elmasri.dependente d

inner join elmasri.funcionario f on (cpf_funcionario = cpf)

order by idade desc;

## QUESTÃO 14


**> ***Prepare um relatório que exiba quantos funcionários cada departamento tem*****

select nome_departamento as departamento ,

count(cpf) as quantos_funcionarios

from elmasri.funcionario f

inner join elmasri.departamento dp on (f.numero_departamento = dp.numero_departamento)

group by nome_departamento;


## QUESTÃO 15


**> ***Como um funcionário pode estar alocado em mais de um projeto, prepare um relatório que exiba o nome completo do funcionário, o departamento desse funcionário e o nome dos projetos em que cada funcionário está alocado. Atenção: se houver algum funcionário que não está alocado em nenhum projeto, o nome completo e o departamento também devem aparecer no relatório.*****

select concat(primeiro_nome,' ', nome_meio,' ', ultimo_nome) as nome_completo_funcionario,

f.numero_departamento as _departamento,

nome_projeto as projeto_alocado

from elmasri.funcionario f

left outer join elmasri.projeto p on (f.numero_departamento = p.numero_departamento);
