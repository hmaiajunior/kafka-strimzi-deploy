# kafka-strimzi-deploy


Os passos abaixo demonstram o ciclo de vida da instalação do kafka no kubernets utilizando o strimzi. Os passos abaixo levam em consideração que o strimzi já está em execução no seu cluster. Isso pode ser validado verificando se o pod do operator está em execução no namespace que você definiu a sua criação (normalmente o namespace kafka)

1 - Apply Kafka.yaml

Você cria um manifesto YAML (Kafka CR) descrevendo o cluster desejado (número de brokers, listeners, storage, etc.) e aplica com kubectl apply.

2 - Observe CRs

O Cluster Operator do Strimzi detecta a criação/alteração do recurso Kafka e começa a planejar as ações necessárias para atingir o estado desejado.

3 - Create Resources

O operador cria recursos Kubernetes nativos:

StatefulSets para brokers e ZooKeeper (ou KRaft)

Services para comunicação interna/externa

ConfigMaps com configurações

Secrets com certificados e credenciais

PVCs para armazenamento persistente

4 - Deploy Pods

O Kubernetes agenda e inicia os pods dos brokers, ZooKeeper, operadores auxiliares (Topic/User Operator) e quaisquer componentes adicionais (Connect, Bridge, Exporters).

5 - Ready for Messages

Com todos os pods prontos e sincronizados, o cluster Kafka está operacional para receber conexões de produtores e consumidores, criar tópicos e processar mensagens.
