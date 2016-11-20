# 1. Protocolo próprio para comunicação

## Status

Proposto

## Contexto

O HDB oferece serviços disponíveis por meio da
interação com clientes. Essa interação deve permitir
a requisição de serviços e o trânsito de dados,
em ambos os sentidos.

## Decisão

Um protocolo próprio será estabelecido com o objetivo
de promover o amplo uso, mesmo em ambientes de recursos
restritos.

## Consequências

- Definição e desenvolvimento de componente específico.
- Definição e desenvolvimento de bibliotecas de acesso para várias linguagens. 
- Não reutiliza ferramentas já disponíveis, por exemplo, se usado HTTP. 
- Eficiência (protocolo personalizado para as necessidades).
- Portabilidade (ambientes com recursos restritos serão considerados).
