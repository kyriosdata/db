
# Visão de camadas
As camadas do HealthDB são indicadas na figura abaixo. Os usos permitidos são exclusivamente entre camadas adjacentes e todos eles estão exibidos na figura. A visão detalhada de cada uma das camadas identifica as responsabilidades de cada camada e os módulos aos quais tais responsabilidades estão atribuídas.

![hdb-layers](https://cloud.githubusercontent.com/assets/1735792/24067912/69290aa4-0b61-11e7-8f5e-b33f1bcac986.png)

***

### Client layer (módulos)
A _Client layer_ compreende vários módulos. O principal módulo é a especificação do protocolo HealthDB (no centro da figura abaixo). Observe que cinco módulos dependem dessa especificação: a interface [HealthDB API](https://github.com/kyriosdata/db/wiki/HealthDB-API) em JavaScript e a implementação do driver correspondente; a interface [HealthDB API](https://github.com/kyriosdata/db/wiki/HealthDB-API) em Java e a correspondente implementação e, por fim, a implementação da HealthDB API no lado do servidor. 

![hdb-layer-client](https://cloud.githubusercontent.com/assets/1735792/24046211/8db1e442-0b00-11e7-9243-c9a6c275a234.png)

Observe ainda os módulos Client [GUI](https://github.com/kyriosdata/db/wiki/Cliente-(gui)) e Client [Console](https://github.com/kyriosdata/db/wiki/Cliente-(console)). O primeiro fornece uma interface gráfica para acesso ao HealthDB via navegador, enquanto o segundo é uma interface baseada na linha de comandos. Esses clientes ilustram como o acesso aos serviços do HealthDB podem ser requisitados por um Sistema de Informação em Saúde (SIS).

Ainda convém ressaltar que a implementação da HealthDB API pode ser realizada em outras linguagens de programação e não apenas em JavaScript e Java, conforme ilustrado.

***

### Application layer
A _Application Layer_ reúne os módulos que implementam a recepção das requisições e o encaminhamento para execução. Essa camada também é responsável pelo acesso a serviços externos.

![hdb-layer-application](https://cloud.githubusercontent.com/assets/1735792/24046166/64a44194-0b00-11e7-80da-66f8650a05f5.png)

Cada um desses módulos estão descritos em [detalhes](https://github.com/kyriosdata/db/wiki/Application-layer).

***

### Domain layer
Os conceitos e serviços oferecidos pelo HealthDB são estão identificados na _Domain layer_, ilustrada abaixo. 

![hdb-layer-domain-subsystems](https://cloud.githubusercontent.com/assets/1735792/24054171/0ef07b72-0b1a-11e7-9c2c-76154c5afbd3.png)

Os módulos apresentados acima estão detalhados [aqui](https://github.com/kyriosdata/db/wiki/Domain-layer).

***

### Storage layer

![hdb-layer-storage](https://cloud.githubusercontent.com/assets/1735792/24068111/7ddacaa6-0b65-11e7-8afe-10c72ab792bb.png)

- [Adapter](https://github.com/kyriosdata/db/wiki/Adaptador). Reúne serviços que permitem "isolar" uma implementação específica dos serviços de armazenamento da camada de dados.
- Native. Implementação personalizada para contemplar apenas os requisitos do HealthDB, por exemplo, não inclui a noção de transação. Inclui _file manager_, _buffer manager_ e componentes similares. O [Codec](https://github.com/kyriosdata/db/wiki/Codec) é um dos principais componentes, responsável pela representação dos dados no formato do HealthDB, assim como o Adapter, responsável pelo processo de empacotamento do resultado de consultas.
- SQL Adapter. Implementa adaptador para um SGBD relacional. Um SGBD SQL é externo (ator) ao HealthDB. Deve existir um adaptador específico para cada SGBD relacional empregado.
- NoSQL Adapter. Implementa adaptador para um SGBD NoSQL. Um SGBD NoSQL é externo (ator) ao HealthDB. Deve existir um adaptador específico para cada SGBD empregado.

***

### Infrastructure layer
Embora não exibida nas figuras acima, a camada de infraestrutura oferece serviços comuns a mais de uma das camadas acima. 
- _File Manager_. Encapsula serviço de acesso a arquivos. Implementação usando Hadoop HDFS deve ser fornecida.
- _RingBuffer_. Encapsula serviço de controle de acesso à memória compartilhada.
- _Logging_. Mantém registro de informações relevantes geradas durante a execução do HealthDB.
- _Log Service_. Serviço responsável por registrar em meio persistente as informações fornecidas no _logging_.
- _Task Manager_. Gerência das várias tarefas executadas concorrentemente pelo HealthDB.
- _Config_. Fornece valores empregados para orientar o comportamento do HealthDB em tempo de execução. 
