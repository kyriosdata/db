# 2. Serviço de log próprio.

## Status

Proposto

## Contexto

O HDB depende de registro de *log* para monitoramento de sua "saúde", além de considerações
sobre portabilidade para dispositivos com recursos limitados e necessidades específicas.

## Decisão

Definir e desenvolver serviços de *log* próprio que contemple as especificidades do HDB.
Serviços como o [log4j](http://logging.apache.org/log4j/2.x/) estabelecem dependência que se deseja evitar,
mas aspectos positivos como o uso de [LMAX Disrupter library](http://lmax-exchange.github.io/disruptor/) são estimulados para o benefício de cenários multi-threaded como
o HDB. 

A ideia é tratar logs como dados e coletar outras informações além de métricas predefinidas. O objetivo é 
responder questões que o negócio não pode antecipar previamente (Technology Radar).

As necessidades deverão ser capturadas em interface própria, com implementação
possivelmente própria usando estratégias como o LMAX Disrupter e outros
onde reconhecido o benefício para o desempenho.

## Consequências

- Reduz eventual dependência de implementação de terceiros.
- Formato deve considerar séries temporais.
- Viabilizar uso direto por ferramentas como Grafana ([aqui](http://grafana.org/)).
