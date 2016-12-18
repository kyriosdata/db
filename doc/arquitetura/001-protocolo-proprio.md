# 1. Protocolo próprio para comunicação

## Status

Proposto

## Contexto

O HealthDB oferece serviços disponíveis por meio da
interação com clientes. Essa interação deve permitir
a requisição de serviços e o trânsito de dados,
em ambos os sentidos, com eficiência. 

## Decisão

Um protocolo próprio será estabelecido com o objetivo
de promover o amplo uso, mesmo em ambientes de recursos
restritos. A figura abaixo permite ilustrar o contexto
de uso do protocolo.

![image](https://cloud.githubusercontent.com/assets/1735792/18794399/bd0cba04-8195-11e6-8763-f9afac71919d.png)

## Consequências

- Definição e desenvolvimento de componente específico.
- Definição e desenvolvimento de bibliotecas de acesso para várias linguagens. 
- Não reutiliza ferramentas já disponíveis, por exemplo, se usado HTTP. 
- Eficiência (protocolo personalizado para as necessidades).
- Portabilidade (ambientes com recursos restritos serão considerados).
