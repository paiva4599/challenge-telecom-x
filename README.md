# Telecom X - Parte 1: Análise Exploratória e Preparação de Dados

<img width="1584" height="396" alt="Challenge (5)" src="https://github.com/user-attachments/assets/b11c81aa-be9a-4f41-9a3e-6bba87f14386" />

## Visão Geral do Projeto
Este projeto corresponde à primeira etapa do desafio da empresa fictícia Telecom X. O objetivo é entender os dados e prepará-los para modelagem preditiva de churn, identificando os fatores que influenciam a evasão de clientes.

As etapas incluem: limpeza, tratamento, análise exploratória, codificação e divisão dos dados, criando uma base para o desenvolvimento de modelos na fase seguinte.

## Estrutura do Projeto
O repositório está organizado da seguinte forma:
- `ChallengeTelecomX.ipynb`: Notebook principal contendo toda a análise exploratória e preparação dos dados.
- `README.md`: Este arquivo, com a visão geral do projeto.

## Tecnologias Utilizadas
Este projeto foi desenvolvido utilizando as seguintes tecnologias:

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Jupyter](https://img.shields.io/badge/jupyter-%23FA0F00.svg?style=for-the-badge&logo=jupyter&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google%20Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=for-the-badge&logo=numpy&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-%23ffffff.svg?style=for-the-badge&logo=Matplotlib&logoColor=black)
![Seaborn](https://img.shields.io/badge/seaborn-%23000000.svg?style=for-the-badge&logo=seaborn&logoColor=white)

## Como executar o notebook
Para replicar a análise, siga os passos abaixo:

1. Clone o repositório:
`git clone https://github.com/paiva4599/challenge-telecom-x.git
cd challenge-telecom-x
`

2. Instale as dependências da primeira célula do notebook
3. Execute o Jupyter Notebook: Abra o arquivo ChallengeTelecomX.ipynb em um ambiente Jupyter e execute as células na ordem apresentada.

## Limpeza e Tratamento de Dados
Para preparar os dados para a análise, foram realizados os seguintes passos de importação, limpeza e tratamento, conforme detalhado no notebook:

### Importação de Bibliotecas e Extração de Dados:
- Foram importadas as bibliotecas pandas para manipulação de dados, e matplotlib e seaborn para visualização.
- Os dados foram extraídos de um arquivo JSON disponível em uma URL pública.
### Normalização de Dados Aninhados:
- O arquivo JSON continha colunas com dados aninhados (customer, phone, internet, e account). Esses dados foram "achatados" e normalizados usando a função `pd.json_normalize()` para que cada informação se tornasse uma coluna distinta no DataFrame.
- O DataFrame resultante foi concatenado para formar uma tabela única e coesa.
### Conversão e Limpeza de Tipos de Dados:
- A coluna `Charges.Total (Gasto Total)` foi identificada como do tipo object (texto) e continha valores não numéricos. Ela foi convertida para um tipo numérico para possibilitar cálculos, e os valores que não puderam ser convertidos foram transformados em nulos (NaN).
- Foram identificados 11 valores nulos na coluna Charges.Total, correspondendo a clientes com 0 meses de contrato (tenure). Presumiu-se que esses eram clientes novos, e o valor nulo foi preenchido com 0.
- A coluna Churn continha valores vazios, que foram removidos para garantir a consistência da análise.
### Transformação de Variáveis:
- Variáveis categóricas binárias que continham "Yes" ou "No" (Churn, Partner, Dependents, PhoneService, PaperlessBilling) foram convertidas para o formato numérico (1 para "Yes" e 0 para "No") para facilitar a análise quantitativa.
- Uma nova coluna, Contas Diarias, foi criada dividindo-se o valor de Charges.Monthly por 30, para fornecer uma visão de custo diário.
### Padronização dos Nomes das Colunas:
- Os nomes das colunas foram traduzidos para o português para tornar o relatório e as visualizações mais claros e compreensíveis (ex: gender para Sexo, tenure para Meses Contrato).
 
## Análise de Dados
Foram realizadas análises por meio de gráficos para verificar a consistência dos Dados tratados. 
### Distribuição Geral do Churn
- A maioria dos clientes permaneceu com a empresa, mas uma parcela significativa (1.869 clientes, ou 26,5%) cancelou o serviço, justificando a necessidade desta análise para entender suas motivações.

<img width="786" height="568" alt="image" src="https://github.com/user-attachments/assets/d8e628db-3f55-42c1-9f73-24e56a0b31f7" />

### Cancelamentos por Variáveis Categóricas
A análise da evasão em diferentes segmentos de clientes mostrou padrões claros:
- **Tipo de Contrato**: Clientes com contrato Mês a Mês (Month-to-month) têm uma taxa de cancelamento drasticamente maior (mais de 1600 clientes) em comparação com aqueles com contratos de Um Ano ou Dois Anos.
- **Serviço de Internet**: A grande maioria dos clientes que cancelaram utilizava o serviço de Fibra Óptica (Fiber optic).
- **Forma de Pagamento**: Clientes que pagam por Cheque Eletrônico (Electronic check) apresentam a maior taxa de churn.
- **Serviços Adicionais**: A ausência de serviços de proteção e suporte está fortemente correlacionada com o churn. Clientes sem Segurança Online (OnlineSecurity), sem Backup Online (OnlineBackup), sem Proteção de Dispositivo (DeviceProtection) e sem Suporte Técnico (TechSupport) cancelaram em números muito maiores do que aqueles que possuíam esses serviços.
### Cancelamentos por Variáveis Binárias
- **Idosos (SeniorCitizen)**: Embora representem uma parcela menor da base de clientes, os idosos têm uma proporção de cancelamento notavelmente alta em relação à sua representatividade.
- **Dependentes e Parceiros**: Clientes que não possuem parceiros e não possuem dependentes são significativamente mais propensos a cancelar.
Fatura Online (PaperlessBilling): Clientes que optam pela fatura online cancelam mais do que aqueles que não a utilizam.

## Conclusão e Insights
A análise dos dados permite extrair as seguintes conclusões sobre o perfil do cliente com maior probabilidade de Churn:

- **O Tipo de Contrato é o Fator Mais Crítico**: A flexibilidade do contrato "Mês a Mês" facilita o cancelamento. Clientes com contratos de longo prazo (1 ou 2 anos) demonstram um comprometimento maior e, consequentemente, uma taxa de churn muito menor.
- **A Qualidade do Serviço de Internet é Determinante**: O alto churn entre clientes de Fibra Óptica, apesar de ser um serviço premium, pode indicar problemas de qualidade, instabilidade, ou uma percepção de custo-benefício desfavorável em comparação com o serviço DSL.
- **Falta de Suporte e Segurança Gera Fricção**: A ausência de serviços como Suporte Técnico e Segurança Online está diretamente ligada à evasão. Isso sugere que clientes que enfrentam problemas técnicos ou se sentem inseguros com o serviço tendem a cancelar se não encontrarem o suporte necessário.
- **O Perfil Demográfico Influencia a Retenção**: Clientes sem laços fortes (sem parceiro ou dependentes) e idosos apresentam maior propensão ao churn. Este grupo pode ser mais sensível a preço, qualidade ou pode ter necessidades de uso diferentes.

## Recomendações
Com base nas conclusões, as seguintes ações são recomendadas para a TelecomX reduzir sua taxa de Churn:

### Incentivar Contratos de Longo Prazo:
- Oferecer descontos progressivos ou benefícios exclusivos (como pacotes de streaming gratuitos ou upgrade de velocidade) para clientes que migrarem do plano "Mês a Mês" para contratos de 1 ou 2 anos.
### Investigar e Melhorar o Serviço de Fibra Óptica:
- Realizar uma análise aprofundada da qualidade da rede de fibra. Coletar feedback de clientes que cancelaram para identificar as causas raiz da insatisfação (ex: instabilidade, velocidade abaixo do prometido, problemas de instalação).
### Agregar Valor com Serviços de Suporte e Segurança:
- Oferecer pacotes que incluam "Segurança Online" e "Suporte Técnico" como um diferencial, especialmente para clientes com contrato de Fibra Óptica.
- Criar uma campanha de marketing para ressaltar os benefícios desses serviços e como eles melhoram a experiência do usuário.
### Desenvolver Ações Focadas em Segmentos de Risco:
- Idosos: Criar planos e ofertas específicas para este público, com preços mais competitivos ou pacotes de serviços simplificados e de fácil utilização.
- Clientes sem Parceiro/Dependentes: Engajar este grupo com ofertas de fidelidade, como descontos em mensalidades após um determinado período de permanência, para fortalecer o vínculo com a marca.
### Revisar o Processo de Pagamento:
- Analisar por que clientes que usam "Cheque Eletrônico" cancelam mais. Pode haver falhas no processo ou falta de opções mais convenientes. Incentivar a adesão ao débito automático ou cartão de crédito, que estão associados a taxas de churn menores, oferecendo um pequeno desconto na fatura.

## Certificado do Desafio
Este projeto faz parte do Challenge ONE - Aprendendo a Fazer ETL, em parceria com a Oracle no programa Oracle Next Education (ONE).

<p align="center"> <img width="300" height="300" alt="TelecomX" src="https://github.com/user-attachments/assets/bea0003c-5ef8-4c46-977f-aceab30404fa" /> </p>

Você pode acompanhar minha publicação sobre este projeto no LinkedIn!

<p> <a href="URL-DO-SEU-POST-NO-LINKEDIN-AQUI"> <img src="https://img.shields.io/badge/Ver%20Postagem-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn Post"> </a> </p>
