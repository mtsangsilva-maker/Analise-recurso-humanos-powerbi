# Análise de Recursos Humanos — Azure Company

## 📊 Sobre o projeto

Este projeto foi desenvolvido como parte do desafio de integração e
processamento de dados utilizando **MySQL Azure e Power BI**.

O objetivo é realizar a coleta dos dados armazenados no banco de dados,
realizar o tratamento e a transformação das informações utilizando o
**Power Query** e, posteriormente, apresentar os principais indicadores
por meio de um dashboard desenvolvido no **Power BI**.

O relatório desenvolvido recebeu o nome de:

**Análise de Recursos Humanos**

---

## 🎯 Objetivo

O projeto tem como objetivo integrar os dados de uma empresa armazenados
em um banco de dados MySQL Azure ao Power BI, realizando as etapas de:

- Coleta dos dados;
- Integração com o banco de dados;
- Tratamento dos dados;
- Transformação das informações;
- Relacionamento entre tabelas;
- Criação de indicadores;
- Construção de visualizações;
- Desenvolvimento de um dashboard para análise dos dados de Recursos
  Humanos.

---

## 🛠️ Tecnologias utilizadas

- **MySQL Azure**
- **Power BI Desktop**
- **Power Query**
- **Power BI Service**

---

## 🗄️ Banco de dados

Foi utilizada a base de dados:

`azure_company`

A base possui informações relacionadas à estrutura organizacional da
empresa, funcionários, departamentos, projetos, horas trabalhadas e
dependentes.

As principais tabelas utilizadas no projeto foram:

- `employee`
- `departament`
- `dept_locations`
- `project`
- `works_on`
- `dependent`

---

# 🔄 Processo de tratamento dos dados

O tratamento dos dados foi realizado utilizando o **Power Query**,
seguindo as etapas propostas no desafio.

## 1. Verificação dos cabeçalhos e tipos de dados

Inicialmente foram verificadas as colunas existentes nas tabelas e seus
respectivos tipos de dados.

Foram realizados ajustes nos tipos de dados quando necessário,
principalmente nos campos numéricos, datas e horas.

---

## 2. Tratamento dos valores monetários

Os valores referentes aos salários dos funcionários foram tratados como
valores numéricos decimais, permitindo a realização de cálculos e
agregações no Power BI.

O campo utilizado foi:

`Salary`

---

## 3. Verificação dos valores nulos

Foi realizada uma análise dos campos que poderiam apresentar valores
nulos.

Na tabela de funcionários, o campo `Super_ssn` foi analisado
especialmente porque representa o supervisor direto do funcionário.

Foi identificado que funcionários sem `Super_ssn` podem representar
funcionários que não possuem um superior na estrutura hierárquica.

---

## 4. Verificação dos funcionários sem gerente

Foi analisada a relação entre o funcionário e seu respectivo supervisor.

Para isso, foi utilizado o campo:

`Super_ssn`

Esse campo foi relacionado ao `Ssn` do funcionário que exerce a função
de gerente.

Posteriormente foi criado o campo:

`Nome Gerente`

permitindo identificar o gerente de cada funcionário.

---

## 5. Verificação dos departamentos e seus gerentes

Foi realizada a verificação dos departamentos e dos respectivos
responsáveis por meio do campo:

`Mgr_ssn`

Os departamentos existentes foram analisados para verificar se havia
algum departamento sem gerente.

---

## 6. Associação dos funcionários aos departamentos

Foi realizada uma **mesclagem de consultas (Merge)** entre a tabela de
funcionários e a tabela de departamentos.

A chave utilizada foi:

`Dno` → `Dnumber`

A tabela de funcionários foi mantida como tabela principal e o nome do
departamento foi incorporado aos seus registros.

Essa transformação permitiu relacionar cada funcionário ao seu
respectivo departamento.

---

## 7. Verificação das horas trabalhadas

A tabela `works_on` foi analisada para verificar as informações
referentes às horas trabalhadas pelos funcionários nos projetos.

O campo utilizado foi:

`Hours`

Também foi realizada a verificação do tipo de dado para permitir
operações de soma e análise no Power BI.

---

## 8. Tratamento das informações de endereço

As informações de endereço dos funcionários estavam reunidas em um
único campo.

O campo `Address` foi separado em diferentes partes, permitindo uma
melhor organização das informações.

Foram criados campos correspondentes às partes do endereço, como:

- Número;
- Rua;
- Cidade;
- Estado.

---

## 9. Criação do nome completo

Os campos:

`Fname`

e

`Lname`

foram combinados para criar o campo:

`Nome Completo`

Essa transformação facilitou a utilização do nome dos funcionários nas
visualizações do dashboard.

---

# 🔗 Mesclagem entre funcionários e departamentos

Foi utilizada a funcionalidade **Mesclar Consultas** do Power Query para
relacionar os funcionários aos seus respectivos departamentos.

A tabela de funcionários foi utilizada como base e relacionada à tabela
de departamentos por meio do código do departamento.

O resultado foi a inclusão do nome do departamento na tabela de
funcionários.

Essa operação preservou os registros dos funcionários e permitiu
enriquecer seus dados com informações provenientes da tabela de
departamentos.

---

# 👨‍💼 Associação dos funcionários aos gerentes

Para identificar os respectivos gerentes dos funcionários, foi criada
uma tabela auxiliar contendo os funcionários que poderiam atuar como
gerentes.

Foi realizada uma mesclagem utilizando:

`Super_ssn` do funcionário

com

`Ssn` do gerente.

Após a mesclagem, foi expandido o nome do gerente e criado o campo:

`Nome Gerente`

Dessa forma, o dashboard consegue apresentar a quantidade de
colaboradores associada a cada gerente.

---

# 📍 Departamento e localização

Foi realizada uma mesclagem entre as informações dos departamentos e
suas respectivas localizações.

A relação foi feita utilizando:

`Dnumber`

como chave comum.

Após a expansão da localização, foram combinados o nome do departamento
e sua localização para criar uma identificação da combinação
departamento-localização.

---

# 🔀 Por que utilizar Mesclar e não Atribuir/Acrescentar?

A funcionalidade **Mesclar** foi utilizada porque o objetivo era
relacionar informações existentes em tabelas diferentes utilizando uma
chave em comum.

Por exemplo, para relacionar funcionários e departamentos, foi
necessário utilizar o código do departamento para trazer o nome do
departamento para os registros dos funcionários.

A funcionalidade **Atribuir/Acrescentar** possui uma finalidade
diferente, pois adiciona as linhas de uma tabela às linhas de outra
tabela.

Portanto, para este projeto, a utilização de **Mesclar** é adequada para
enriquecer os registros existentes com informações relacionadas de outras
tabelas.

---

# 👥 Funcionários por gerente

Foi realizado um agrupamento para identificar a quantidade de
funcionários subordinados a cada gerente.

Essa informação foi utilizada posteriormente na construção do gráfico
de colaboradores por gerente no dashboard.

---

# 🧹 Remoção de colunas desnecessárias

Após a realização das transformações e mesclagens necessárias, foram
avaliadas as colunas existentes nas tabelas.

As informações que não eram necessárias para o tratamento ou para as
análises finais foram removidas, mantendo os dados relevantes para o
modelo e para o dashboard.

---

# 📊 Dashboard — Análise de Recursos Humanos

Após o tratamento dos dados no Power Query, foi desenvolvido um
dashboard em uma única página no Power BI.

O objetivo do dashboard é apresentar uma visão resumida das principais
informações relacionadas aos funcionários da empresa.

## Indicadores

O dashboard apresenta três cartões principais:

### Total de Funcionários

Apresenta a quantidade total de funcionários cadastrados na base.

### Salário Médio

Apresenta a média dos salários dos funcionários.

### Total de Horas Trabalhadas

Apresenta a soma das horas registradas na tabela `works_on`.

---

# 🥧 Funcionários por Sexo

Foi criado um **gráfico de pizza** para apresentar a distribuição dos
funcionários de acordo com o campo:

`Sex`

O campo `Ssn` é utilizado como contagem para representar a quantidade de
funcionários em cada categoria.

---

# 📊 Salário Médio por Departamento

Foi criado um **gráfico de barras** para apresentar o salário médio dos
funcionários agrupado por departamento.

Foram utilizados:

- `Dname` como departamento;
- `Salary` utilizando a agregação **Média**.

Essa visualização permite observar a média salarial de cada departamento
da empresa.

---

# 👨‍💼 Colaboradores por Gerente

Foi criado um **gráfico de colunas** para apresentar a quantidade de
colaboradores associados a cada gerente.

A informação utilizada é o campo:

`Nome Gerente`

Essa visualização permite analisar a distribuição dos colaboradores
dentro da estrutura hierárquica da empresa.

---

# 📋 Tabela de funcionários

Também foi criada uma tabela detalhada para apresentar informações
individuais dos funcionários.

Entre as informações apresentadas estão:

- Nome;
- Departamento;
- Gerente;
- Salário.

Essa tabela complementa os gráficos e permite consultar informações
detalhadas dos colaboradores.

---

# 📈 Resultado final

O resultado do projeto é um dashboard de **Análise de Recursos Humanos**
que reúne informações de diferentes tabelas do banco de dados em uma
única visão.

O relatório permite analisar:

- Quantidade de funcionários;
- Salário médio;
- Horas trabalhadas;
- Distribuição dos funcionários por sexo;
- Salário médio por departamento;
- Quantidade de colaboradores por gerente;
- Informações detalhadas dos funcionários.

---

# 💡 Conclusão

O desenvolvimento deste projeto possibilitou a integração dos dados do
MySQL Azure com o Power BI e a aplicação de técnicas de tratamento e
transformação utilizando o Power Query.

As mesclagens realizadas permitiram relacionar funcionários,
departamentos, gerentes e localizações, transformando os dados originais
em informações mais adequadas para análise.

Após o tratamento, os dados foram utilizados para construir o relatório
**Análise de Recursos Humanos**, reunindo indicadores e visualizações
em uma única página.

O projeto demonstra o fluxo de trabalho de coleta, transformação e
visualização de dados utilizando MySQL Azure e Power BI.
