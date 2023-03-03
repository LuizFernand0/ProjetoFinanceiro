
### Documentacao:

<div hidden>
```
@startuml firstDiagram

Title Fluxo API Github
Header Arquitetura swap challenge

control Client #red
control Api #blue
queue RabbitMQ #orange
control Worker #green
control Schedule #lime
database MySQL #yellow

'fluxo de ida
Client -> Api: Solicita relatorio
Api -[#blue]> RabbitMQ : Envio fila: request.issue.queue
Worker <[#blue]- RabbitMQ  : Leitura fila : request.issue.queue
RabbitMQ -[#blue]> RabbitMQ : Envio fila : deadletter.queue
Worker -[#blue]> MySQL : Grava relatorio

'fluxo de volta
Schedule <[#green]- MySQL : Leitura: relatorios
Schedule -[#green]> Client: Envia webhook
@enduml
```
</div>
  
![](firstDiagram.svg)
