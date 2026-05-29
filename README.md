# Integração de Dados com MySQL Azure e Transformação no Power BI

## Sobre o Projeto

Este projeto foi desenvolvido como parte do desafio **Integrando Dados com MySQL Azure e Transformando com Power BI**.

O objetivo foi criar uma instância MySQL na Azure, integrar os dados ao Power BI e realizar um processo completo de ETL (Extração, Transformação e Carga), preparando a base para análises e futura modelagem dimensional.

---

## Tecnologias Utilizadas

* Microsoft Azure Database for MySQL
* MySQL Workbench
* Power BI Desktop
* Power Query

---

## Competências Demonstradas

* Integração de dados entre MySQL e Power BI
* ETL com Power Query
* Tratamento de dados nulos
* Ajuste de tipos de dados
* Junções (Merge)
* Agrupamentos e agregações
* Limpeza e padronização de dados
* Preparação de dados para modelo estrela
* Modelagem de dados para Business Intelligence

---

## Etapas do Projeto

### 1. Criação do Ambiente

* Criação de uma instância MySQL no Microsoft Azure.
* Configuração das regras de firewall para acesso externo.
* Conexão ao banco utilizando MySQL Workbench.
* Importação da base de dados disponibilizada para o desafio.

### 2. Integração com Power BI

* Conexão do Power BI à instância MySQL hospedada na Azure.
* Importação das tabelas para o Power Query.

---

## Transformações Realizadas

### Validação dos Dados

Foram verificados:

* Cabeçalhos das tabelas
* Tipos de dados
* Campos numéricos e monetários
* Valores nulos

### Tratamento de Valores Nulos

Foi realizada a análise dos registros nulos presentes na base.

Observou-se que colaboradores sem valor em **Super_ssn** correspondiam aos gerentes dos departamentos, não sendo necessária a exclusão desses registros.

Também foi realizada a verificação da existência de departamentos sem gerente associado.

### Conversão de Tipos de Dados

Os campos monetários foram convertidos para tipos numéricos adequados, permitindo cálculos e agregações futuras.

### Verificação das Horas dos Projetos

Foi realizada a conferência das horas registradas nos projetos para garantir consistência dos dados.

### Separação de Colunas Complexas

Campos compostos foram ajustados para facilitar futuras análises e relacionamentos.

---

## Mesclagem de Tabelas

### Colaboradores e Departamentos

Foi realizada uma mesclagem entre as tabelas **Employee** e **Department** utilizando:

```text
Employee.Dno = Department.Dnumber
```

Tipo de junção utilizado:

```text
Left Outer Join
```

Essa transformação permitiu associar cada colaborador ao respectivo departamento.

---

### Colaboradores e Gerentes

Foi realizada uma segunda mesclagem para identificar o gerente responsável por cada colaborador.

Relacionamento utilizado:

```text
Department.Mgr_ssn = Employee.Ssn
```

Após a expansão da tabela relacionada, foi possível obter o nome do gerente correspondente a cada colaborador.

---

### Consolidação dos Nomes

As colunas de nome e sobrenome foram unificadas em uma única coluna de identificação dos colaboradores, facilitando a leitura e análise dos dados.

---

### Departamento e Localização

Foi realizada a mesclagem entre as tabelas de departamentos e localizações, criando combinações únicas entre departamento e localização.

Exemplos:

* Research - Houston
* Research - Bellaire
* Administration - Stafford

Essa transformação auxilia futuras implementações de modelo estrela.

---

## Agrupamento dos Dados

Os dados foram agrupados por gerente para identificar a quantidade de colaboradores sob responsabilidade de cada gestor.

Exemplo:

| Gerente          | Quantidade de Colaboradores |
| ---------------- | --------------------------- |
| Franklin Wong    | 4                           |
| Jennifer Wallace | 3                           |
| James Borg       | 1                           |

---

## Remoção de Colunas Desnecessárias

Após as transformações, foram removidas colunas intermediárias e atributos que não seriam utilizados no relatório final.

Exemplos:

* Minit
* Address
* Bdate
* Sex
* Super_ssn
* Campos auxiliares criados durante as mesclagens

Essa etapa teve como objetivo simplificar o modelo de dados e melhorar a organização do relatório.

---

## Por que Utilizar Mesclar e Não Acrescentar?

A operação **Mesclar (Merge)** foi utilizada porque o objetivo era combinar informações complementares entre tabelas relacionadas por chaves em comum.

A operação **Acrescentar (Append)** não seria adequada neste cenário, pois sua finalidade é empilhar registros de tabelas com estruturas semelhantes.

Como o objetivo era enriquecer os registros existentes com informações adicionais, a operação de mesclagem foi a abordagem correta.

---

## Resultado Final

Ao final do processo foi obtida uma base de dados limpa, organizada e preparada para análises no Power BI.

As transformações realizadas permitiram relacionar colaboradores, departamentos, gerentes e localizações, criando uma estrutura adequada para visualização e futuras etapas de modelagem dimensional.

## Dashboard Final

![Dashboard Final](images/dashboard_final.png)
