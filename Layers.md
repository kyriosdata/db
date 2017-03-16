
# Visão de camadas
As camadas do HealthDB são indicadas na figura abaixo. Os usos permitidos são exclusivamente entre camadas adjacentes e todos eles estão exibidos na figura. A visão detalhada de cada uma das camadas identifica as responsabilidades de cada camada e os módulos aos quais tais responsabilidades estão atribuídas.

![hdb-layers](https://cloud.githubusercontent.com/assets/1735792/24011441/8cdced5c-0a59-11e7-8527-4537c204a8f4.png)

Os módulos de cada uma das camadas são identificados abaixo. 

#### User Interface layer (módulos)
Os módulos da _User Interface Layer_ são exibidos na figura abaixo. Cinco módulos implementam a interface HealthDB API, empregando linguagens distintas. O módulo Client Console que oferece acesso às funções administrativas, inclusive consultas, do HealthDB e o módulo com conjunto de funções similar, mas acessado via _browser_. 

![hdb-layer-client](https://cloud.githubusercontent.com/assets/1735792/22626068/393e3e76-eb8c-11e6-9042-5e0dcfe9697f.png)

Detalhes de alguns módulos:

- Cliente Administrativo ([CAD](https://github.com/kyriosdata/db/wiki/CAD-(cliente))). Meio de acesso de usuários humanos às funções oferecidas pelo HealthDB, por exemplo, criação de contas e monitoramento, além da execução de consultas. Há previsão de implementação do CAD em duas versões: (a) [gráfica](https://github.com/kyriosdata/db/wiki/Cliente-(gui)) e (b) [console](https://github.com/kyriosdata/db/wiki/Cliente-(console)).
- [HealthDB API](https://github.com/kyriosdata/db/wiki/HealthDB-API). Clientes (softwares) interagem com o HealthDB trocando mensagens por meio dessa API. Convém destacar que toda informação que trafega para/do HealthDB faz uso dessa API.

#### Application layer
Os módulos da _Application Layer_ são apresentados no diagrama abaixo. 

![hdb-layer-application](https://cloud.githubusercontent.com/assets/1735792/22622583/3503510a-eb25-11e6-914d-52deff7ab441.png)

Detalhes:
- _HealthDB Endpoint_. Implementação do lado "servidor" da [HealthDB API](https://github.com/kyriosdata/db/wiki/HealthDB-API).
- Autenticação e Autorização ([A2](https://github.com/kyriosdata/db/wiki/Autentica%C3%A7%C3%A3o-e-Autoriza%C3%A7%C3%A3o-(A2))).
- Auditoria.
- Conexão com serviços externos utilizados pelo HealthDB, por exemplo, CNS, CNES e outros. 
- [_Work Manager_](https://github.com/kyriosdata/db/wiki/Work-Manager). Decide se o processamento de uma requisição deve ser iniciada imediatamente ou aguardar até que recursos considerados necessários estejam disponíveis para serem alocados à requisição. Adicionalmente, estabelece a ligação entre _worker thread_ usada para tratar a requisição (lógico) e a correspondente implementação (física) usando _threads_ em Java, _lightweight thread_, um processo ou outro mecanismo, inclusive o uso de _pool_ desses recursos físicos.
- _Use Case Manager_. O HealthDB apresenta aos clientes alguns casos de uso: importar, exportar dados, acréscimo de arquétipo e, talvez o mais comum, consulta AQL. 
- _Session Manager_. Responsável por manter o estado da conexão de um cliente com o HealthDB.  
- [Conversores](https://github.com/kyriosdata/db/wiki/Conversores). Assegura representação do formato empregado pelo HealthDB em XML, JSON e outros, e vice-versa.

#### Data layer
Os módulos da _Data layer_ são apresentados na figura abaixo. 

![hdb-layer-data](https://cloud.githubusercontent.com/assets/1735792/22618587/7257d7aa-eac7-11e6-9645-b095e86b18ca.png)

Detalhes:

- [ADL Compiler](https://github.com/kyriosdata/db/wiki/Compilador-ADL). Responsável por receber um arquétipo descrito em ADL e produzir a representação interna correspondente.
- [AQL Compiler](https://github.com/kyriosdata/db/wiki/Compilador-AQL). Responsável por produzir a representação interna correspondente a uma consulta.
- Schema Generator ([DSG](https://github.com/kyriosdata/db/wiki/Data-Schema-Generator-(DSG))). Módulo que recebe a representação interna de um arquétipo produzida pelo compilador de ADL e produz: (a) um esquema em conformidade com a _storage engine_ a ser utilizada pelo HealthDB e (b) metadados correspondentes. 
- Execution Plan Generator ([DQG](https://github.com/kyriosdata/db/wiki/Data-Query-Generator-(DQG))). Responsável por converter a representação interna de uma consulta, em conformidade com a representação interna do esquema (metadados) em consulta que pode ser executada pela _storage engine_.
- [Storage Engine Conector](https://github.com/kyriosdata/db/wiki/Storage-Engine-Connector-(SEC)). Conexão com a _storage engine_ usada. Esse é o componente que, de fato, repassa para o _storage manager_ requisições. No sentido inverso, o conector faz uso de um conversor dos dados produzidos pela execução do _storage engine_ no formato empregado internamente pelo HealthDB.
- [Metadata Manager](https://github.com/kyriosdata/db/wiki/Metadata). Oferece serviços para persistência de informações sobre dados. 
- [Keyword Processor](https://github.com/kyriosdata/db/wiki/Palavras-chave). Módulo que produz, a partir de um conjunto de palavras-chave, uma consulta AQL correspondente. 

#### Storage engine layer
- [Adaptador](https://github.com/kyriosdata/db/wiki/Adaptador). Realiza várias funções que permitem "isolar" uma implementação específica dos serviços de armazenamento da camada de dados.
- Native. Implementação personalizada para contemplar apenas os requisitos do HealthDB, por exemplo, não inclui a noção de transação. Inclui _file manager_, _buffer manager_ e componentes similares. O [Codec](https://github.com/kyriosdata/db/wiki/Codec) é um dos principais componentes, responsável pela representação dos dados no formato do HealthDB, assim como o Adapter, responsável pelo processo de empacotamento do resultado de consultas.
- SQL. Representa um SGBD relacional. Esse componente é externo ao HealthDB e, caso empregado, demanda implementação de [Adaptador](https://github.com/kyriosdata/db/wiki/Adaptador) específico. 
- NoSQL. Representa um SGBD NoSQL. Esse componente é externo ao HealthDB. Caso seja empregado, demanda implementação de [Adaptador](https://github.com/kyriosdata/db/wiki/Adaptador) específico.

#### Infrastructure layer
Embora não exibida nas figuras acima, a camada de infraestrutura oferece serviços comuns a mais de uma das camadas acima. 
- _File Manager_. Encapsula serviço de acesso a arquivos. Implementação usando Hadoop HDFS deve ser fornecida.
- _RingBuffer_. Encapsula serviço de controle de acesso à memória compartilhada.
- _Logging_. Mantém registro de informações relevantes geradas durante a execução do HealthDB.
- _Log Service_. Serviço responsável por registrar em meio persistente as informações fornecidas no _logging_.
- _Task Manager_. Gerência das várias tarefas executadas concorrentemente pelo HealthDB.
- _Config_. Fornece valores empregados para orientar o comportamento do HealthDB em tempo de execução. 
