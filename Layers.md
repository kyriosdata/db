
# Visão de camadas
As camadas do HealthDB são indicadas na figura abaixo. Os usos permitidos são exclusivamente entre camadas adjacentes e todos eles estão exibidos na figura. A visão detalhada de cada uma das camadas identifica as responsabilidades de cada camada e os módulos aos quais tais responsabilidades estão atribuídas.

![hdb-layers](https://cloud.githubusercontent.com/assets/1735792/24011441/8cdced5c-0a59-11e7-8527-4537c204a8f4.png)

***

### Client layer (módulos)
A _Client layer_ compreende vários módulos. O principal módulo é a especificação do protocolo HealthDB (no centro da figura abaixo). Observe que cinco módulos dependem dessa especificação: a interface [HealthDB API](https://github.com/kyriosdata/db/wiki/HealthDB-API) em JavaScript e a implementação do driver correspondente; a interface [HealthDB API](https://github.com/kyriosdata/db/wiki/HealthDB-API) em Java e a correspondente implementação e, por fim, a implementação da HealthDB API no lado do servidor. 

![hdb-layer-client](https://cloud.githubusercontent.com/assets/1735792/24012580/45947772-0a5d-11e7-8f2d-599e5b71fb1d.png)

Observe ainda os módulos Client [GUI](https://github.com/kyriosdata/db/wiki/Cliente-(gui)) e Client [Console](https://github.com/kyriosdata/db/wiki/Cliente-(console)). O primeiro fornece uma interface gráfica para acesso ao HealthDB via navegador, enquanto o segundo é uma interface baseada na linha de comandos. Esses clientes ilustram como o acesso aos serviços do HealthDB podem ser requisitados por um Sistema de Informação em Saúde (SIS).

Ainda convém ressaltar que a implementação da HealthDB API pode ser realizada em outras linguagens de programação e não apenas em JavaScript e Java, conforme ilustrado.

***

### Application layer
A _Application Layer_ reúne os módulos que implementam a recepção das requisições e o encaminhamento para execução. Essa camada também é responsável pelo acesso a serviços externos.

![hdb-layer-application](https://cloud.githubusercontent.com/assets/1735792/24046166/64a44194-0b00-11e7-80da-66f8650a05f5.png)

Cada um desses módulos estão descritos em [detalhes](https://github.com/kyriosdata/db/wiki/Application-layer).

***

### Data layer
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

***

### Storage engine layer
- [Adaptador](https://github.com/kyriosdata/db/wiki/Adaptador). Realiza várias funções que permitem "isolar" uma implementação específica dos serviços de armazenamento da camada de dados.
- Native. Implementação personalizada para contemplar apenas os requisitos do HealthDB, por exemplo, não inclui a noção de transação. Inclui _file manager_, _buffer manager_ e componentes similares. O [Codec](https://github.com/kyriosdata/db/wiki/Codec) é um dos principais componentes, responsável pela representação dos dados no formato do HealthDB, assim como o Adapter, responsável pelo processo de empacotamento do resultado de consultas.
- SQL. Representa um SGBD relacional. Esse componente é externo ao HealthDB e, caso empregado, demanda implementação de [Adaptador](https://github.com/kyriosdata/db/wiki/Adaptador) específico. 
- NoSQL. Representa um SGBD NoSQL. Esse componente é externo ao HealthDB. Caso seja empregado, demanda implementação de [Adaptador](https://github.com/kyriosdata/db/wiki/Adaptador) específico.

***

### Infrastructure layer
Embora não exibida nas figuras acima, a camada de infraestrutura oferece serviços comuns a mais de uma das camadas acima. 
- _File Manager_. Encapsula serviço de acesso a arquivos. Implementação usando Hadoop HDFS deve ser fornecida.
- _RingBuffer_. Encapsula serviço de controle de acesso à memória compartilhada.
- _Logging_. Mantém registro de informações relevantes geradas durante a execução do HealthDB.
- _Log Service_. Serviço responsável por registrar em meio persistente as informações fornecidas no _logging_.
- _Task Manager_. Gerência das várias tarefas executadas concorrentemente pelo HealthDB.
- _Config_. Fornece valores empregados para orientar o comportamento do HealthDB em tempo de execução. 
