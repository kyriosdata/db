
# Visão de camadas
As camadas do HealthDB são indicadas na figura abaixo. Os usos permitidos são exclusivamente entre camadas adjacentes e todos eles estão exibidos na figura.

![hdb-layers](https://cloud.githubusercontent.com/assets/1735792/24067912/69290aa4-0b61-11e7-8f5e-b33f1bcac986.png)

Cada uma das camadas é composta por módulos e dos usos permitidos entre eles. A [_Client Layer_](https://github.com/kyriosdata/db/wiki/Client-layer) é a camada de aplicativos clientes do HealthDB e da implementação da comunicação de um cliente com o HealthDB. A [_Application Layer_](https://github.com/kyriosdata/db/wiki/Application-layer) reúne os módulos que implementam a recepção das requisições recebidas dos clientes, as encaminha para execução e gerencia sessões, além de fazer acesso a serviços externos. A [_Domain Layer_](https://github.com/kyriosdata/db/wiki/Domain-layer) implementa os conceitos principais como o de arquétipos, consultas AQL e outros, sem fazer acesso a nenhum módulo externo. A [_Storage Layer_](https://github.com/kyriosdata/db/wiki/Storage-layer) realiza operações sobre os dados como o armazenamento e a recuperação. A [_Infrastructur Layer_](https://github.com/kyriosdata/db/wiki/Infrastructure-layer) reúne módulos cujas funções compartilhadas por duas ou mais camadas. 
