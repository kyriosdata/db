# 2. Serviço de log próprio.

## Status

Proposto

## Contexto

O HDB depende de registro de *log* para monitoramento de sua "saúde". 

## Decisão

Serviços de *log* como log4j estabelecem dependência que se deseja evitar. 
As necessidades deverão ser capturadas em interface própria, com implementação
possivelmente própria (sem necessidade de recorrer a implementações amplamente
utilizadas).

## Consequências

- Reduz eventual dependência de implementação de terceiros.
- Formato deve considerar séries temporais.
- Viabilizar uso direto por ferramentas como Grafana ([aqui](http://grafana.org/)).
