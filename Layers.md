
# Visão de camadas
As camadas do HealthDB são indicadas na figura abaixo. Os usos permitidos são exclusivamente entre camadas adjacentes e todos eles estão exibidos na figura.

![hdb-layers](https://cloud.githubusercontent.com/assets/1735792/24067912/69290aa4-0b61-11e7-8f5e-b33f1bcac986.png)

Cada uma das camadas é composta por módulos e dos usos permitidos entre eles. A [_Client Layer_](https://github.com/kyriosdata/db/wiki/Client-layer) é a camada de aplicativos clientes do HealthDB e da implementação da comunicação de um cliente com o HealthDB. A [_Application Layer_](https://github.com/kyriosdata/db/wiki/Application-layer) reúne os módulos que implementam a recepção das requisições recebidas dos clientes, as encaminha para execução e gerencia sessões, além de fazer acesso a serviços externos. A [_Domain Layer_](https://github.com/kyriosdata/db/wiki/Domain-layer) implementa os conceitos principais como o de arquétipos, consultas AQL e outros, sem fazer acesso a nenhum módulo externo. A [_Storage Layer_](https://github.com/kyriosdata/db/wiki/Storage-layer) realiza operações sobre os dados como o armazenamento e a recuperação.

***

### Application layer
A [_Application Layer_](https://github.com/kyriosdata/db/wiki/Application-layer) reúne os módulos que implementam a recepção das requisições e o encaminhamento para execução. Essa camada também é responsável pelo acesso a serviços externos.

![hdb-layer-application](https://cloud.githubusercontent.com/assets/1735792/24046166/64a44194-0b00-11e7-80da-66f8650a05f5.png)

Cada um desses módulos estão descritos em [detalhes](https://github.com/kyriosdata/db/wiki/Application-layer).

***

### Infrastructure layer
Embora não exibida nas figuras acima, a camada de infraestrutura oferece serviços comuns a mais de uma das camadas acima. 
- _File Manager_. Encapsula serviço de acesso a arquivos. Implementação usando Hadoop HDFS deve ser fornecida.
- _RingBuffer_. Encapsula serviço de controle de acesso à memória compartilhada.
- _Logging_. Mantém registro de informações relevantes geradas durante a execução do HealthDB.
- _Log Service_. Serviço responsável por registrar em meio persistente as informações fornecidas no _logging_.
- _Task Manager_. Gerência das várias tarefas executadas concorrentemente pelo HealthDB.
- _Config_. Fornece valores empregados para orientar o comportamento do HealthDB em tempo de execução. 
