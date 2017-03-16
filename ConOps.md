# Contexto de operação (ConOps)
Abaixo segue a visão operacional do HealthDB na perspectiva dos seus usuários.

### Contexto do sistema

![hdb-context](https://cloud.githubusercontent.com/assets/1735792/23322571/568f1162-fac3-11e6-975c-a2d540df0861.png)

| Ator           |   Descrição  |
|:--------------:|----------------|
|Cliente   | Software que faz uso dos recursos do HealthDB. É o principal ator cuja interação típica pode ser modelada pelo envio de consultas (AQL) e recuperação dos resultados (ResultSet) por meio do uso de HealthDB API. |
|DBA/Developer      | Indivíduo que mantém o HealthDB em funcionamento (requisita funções de administração do HealthDB), além de requisitar serviços típicos durante o desenvolvimento, como a execução de consultas AQL. |
|Sistema externo | Sistema com o qual o SISB interage, tanto para enviar quanto para receber informações em conformidade com os padrões adotados pelo Brasil.|


### Casos de uso

![hdb-context](https://cloud.githubusercontent.com/assets/1735792/24000856/3b6f1df0-0a3b-11e7-967a-344729a23141.png)

| Caso de Uso    |   Descrição  |
|--------------|----------------|
|Generate auditor reports| Gerar relatórios úteis aos propósitos de auditoria.|
|Import/export data|Permite a incorporação de dados baseados em arquétipos e a correspondente exportação.|
|Execute query| Executa consultas AQL.|
|Manage archetypes| Permite acrescentar, remover arquétipos geridos pelo HealthDB.|

### Modelo do domínio
O HealthDB executa funções (Work) de importação/exportação de dados e consultas (Query), dentre outras. Cada uma delas associada a um usuário (User) que deve estar devidamente autenticado (Access Control) para fazer uso do banco de dados (Database) em questão. Tais funções produzem um resultado (ResultSet). Em geral, trata-se de dados de saúde (RMObject), pertinentes a um Registro Eletrônico em Saúde (EHR) baseados em um ou mais arquétipos. Em tempo, cada EHR é pertinente a um paciente (Patient) cujos dados demográficos (Demographic) são mantidos "separados" das informações clínicas propriamente ditas.

![hdb-domain](https://cloud.githubusercontent.com/assets/1735792/23341779/139f8a4c-fc2d-11e6-89c8-7211d11bb13f.png)


### Visão operacional
O HealthDB é um SGBD que oferece serviços a um Sistema de Informação em Saúde (SIS) por meio da [HealthDB API](https://github.com/kyriosdata/db/wiki/HealthDB-API). 

![hdb-operational](https://cloud.githubusercontent.com/assets/1735792/24010300/39ba8efc-0a56-11e7-8e74-1454a0aa265b.png)

No cenário acima um servidor atende requisições de vários terminais simultanemente. O SISB, contudo, deve ser capaz de operar em outros cenários, por exemplo, no qual o usuário interage com um computador no qual o SISB está em execução, sem conexão com serviço remoto.

### Restrições

- Fazer uso exclusivo de tecnologia "livre" de royalties. 
- O SISB deve apresentar "baixo" custo de implantação e também "baixo" custo de manutenção. O custo deve ser monitorado e, na presença de mudança, aprovado pela patrocinadora do projeto. Naturalmente, o custo é uma função de várias variáveis, inclusive da quantidade de acessos concorrentes por unidade de tempo para os quais o serviço deve se manter estável. 

