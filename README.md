<h1 align="center">ESTUDO RABBITMQ</h1>


![RabbitMQ](https://img.shields.io/badge/Rabbitmq-FF6600?style=for-the-badge&logo=rabbitmq&logoColor=white)

<h3><P><b> O QUE É ?</b></p></h3>

É um message Broker, nada mais que um software de troca de mensagens, realizando comunicação entre sistemas ou diferentes projetos.

<b>Exemplo:</b> Em um app de pedidos de fast food utilizando microsserviços, através do RabbitMq, é possível realizar a comunicação entre diferentes partes do app utilizando a mensageria. 

Como o microsserviço de pagamento irá saber qual cadastro está fazendo o pedido e quanto terá que pagar? Utilizando o RabbitMq.

O RabbitMq da suporte ao <b>AMPQ</b> (Advanced messaging queue protocol)

<img src="https://github.com/JorgeAlbano/estudo-rabbitmq/assets/85715273/d5504104-73bf-4240-b6ae-6797674387df" width= 600px />

É um protocolo simples de mensagem, o Publisher é quem publica, a Queue (fila) é a rota da mensagem e o Consumer é quem recebe a mensagem.

Mas o publisher nunca publica diretamente em uma Queue, é utilizado uma Exchange.

<img src="https://github.com/JorgeAlbano/estudo-rabbitmq/assets/85715273/9e8d626d-e1e0-4cc1-ae26-3275731f42ae" width= 600px />

A <b>Exchange</b> recebe a mensagem, analisa e distribui para as Queue (filas). Há diversas configuracoes de Exchanges, para diversos tipos de aplicações. Mas antes de falar sobre os tipos de Exchanges, é necessário entender sobre Binding.

<img src="https://github.com/JorgeAlbano/estudo-rabbitmq/assets/85715273/c1d51c34-4fff-4833-98d7-0432f80931bc" width= 600px />

<b>Binding</b> é uma configuração imposta na Queue(fila), de acordo com a configuração realizada nas filas através da routingKey a Exchange envia ou não a mensagem para a fila.

<h3><b><p>Tipos de Exchanges: </p></b></h3>

<b>Direct:</b> Utilizada quando deseja-se enviar mensagens para um consumidor específico. Enviando uma routingKey junto com a mensagem, para a Exchange identificar qual fila enviará ao consumidor correto.

<b>Fanout:</b> Envia a mensagem para todas as filas configuradas com o mesmo Binding.

<b>Topic:</b> Muito flexível, pode-se nomear Binding com regras ou padrões personalizados. Exemplo, primeira mensagem enviar apenas para duas filas, na segunda mensagem enviar apenas para uma fila. Utilizando Binding key com nomes diferentes.

<b>Header:</b> Menos usada, ignora o Routing Key e passa no próprio cabeçalho da mensagem, para qual Binding Key deve ser encaminhada.

<h3><b><p>Por dentro do RabbitMq</p></b></h3>

<b>RabbitListener:</b> É quem consome as mensagens dentro de uma fila utilizando a annotation @RabbitListener.

<b>Message TTL:</b> É o tempo determinado, caso a mensagem não seja consumida, seja deletada.

<b>OverFlow Behavior:</b> Configuração caso houver um transbordo de mensagens dentro da fila

<b>DLQ:</b> Dead Letter Queue, onde mensagens que não foram possíveis de serem entregues para as filas destinadas, são enviadas.

<b>DLX:</b> Dead Letter Exchange, é o "encaminador" da mensagem para a DLQ.

No RabbitMq um cluster de alta disponibilidade é importante, pelo fato de, inúmeras mensagens para ser entregues em uma mesma fila, com um curto espaço de tempo. Pode-se perder mensagens ou entregue em fora de ordem e isso seria um problema grave para a aplicação de mensageria.
