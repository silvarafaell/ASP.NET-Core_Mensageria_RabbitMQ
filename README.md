Curso Mensageria com RabbitMQ e ASP.NET Core no nextwave(LuisDEV)

### O que é Mensageria ?
 - Antes de falar sobre mensageria, é importante entender sobre a forma de comunicação tradicional, estilo Request-Response.
 - Nela, um componente de software realiza uma requisição a um servidor, aguardando a sua resposta.
 - Concluindo o processamento da requisição, o servidor retorna a resposta
 - Esse processo funciona muito bem na grande maioria dos cenários. Porém, em cenários onde o processamento do servidor tem várias etapas, o tempo de resposta poderá ser alto, além  de ser mais vulnerável a falhas em componentes em que o servidor dependa
 - Componentes podem falhar, a rede pode se torna instavel e falhar, enfim, falhas fazem parte da comunicação entre componentes de software!
 - Com esse cenário, a mensageria se tornou uma excelente alternativa para comunicação desacoplada entre componentes
 - Mensageria é uma maneira de permitir a comunicação entre diferentes sistemas ou componentes de software de forma desacoplada
 - Comunicação desacoplada significa que sistemas podem interagir entre si sem ter conhecimento um do outro, o que contribui para a modularidade e independência dos componentes
 - Este método de comunicação é essencial em arquiteturas modernas de microserviços, onde várias aplicações precisam se comunicar de forma eficiente e resiliente.
 - Essa comunicação é realizada principalmente através do envio de mensagens - pacotes de dados que contem informações.
 - Em vez de se comunicarem diretamente uns com os outros, os componentes do software enviam mensagens para uma fila, que é como se fosse uma "caixa de correio"
 - Apos isso, elas continuam seus processos sem esperar uma resposta imediata após a publicação da mensagem.
 - As mensagens então são retiradas por outras aplicações, que podem processá-las de acordo com as suas operações e regras de negócio.
 - Benefícios da Mensageria
   - Permite que sistemas distribuidos sejam desenvolvidos, implantados, e escalados de forma independente
   - Melhora a resilência do sistema, pis uma falha em um componente não afeta diretamente os outros
   - Melhora a performance em fluxo de operações com multiplos passos, pois permite que nem todos precisem ser feitos na requisição inicial
   
### O que é RabbitMQ
 - RabbitMQ é uma ferramenta de mensageria open-source bastante popular
 - Possui suporte a vários protocolos de mensageria e que pode ser facilmente conectado a diversos sistemas, incluindo aplicações .NET
 - Ele é conhecido por ser leve e fácil de publicar tanto on premise quanto na nuvem
 - Tambem suporta requisitos de alta escalabilidade e disponibilidade
 - Finalmente, pode ser executado em diferentes sistemas operacionais e ambientes de nuvem.
 - Em uma comunicação através de mensageria, o Rabbit atua como intermediário na troca de mensagens entre os produtos e consumidores
 - O produtor é a aplicação que gera e envia mensagens para uma fila
 - Já o consumidor é a aplicação que recebe e processa essas mensagens
 - Os principais conceitos relacionados ao RabbitMQ são:
   - Exchanges
   - Filas
   - Bindings
   - Routings Keys
 - O RabbitMQ oferece diversas funcionalidades, como:
   - Roteamento flexivel de mensagens
   - Dead Letter Queue
   - Confirmação de mensagens
   - Clusterização para alta disponibilidade
   - API HTTP, interface de usuário e linha de comando para gerenciamento e monitoramento
   - Plugins
   
### Arquitetura do RabbitMQ
 - Os principais conceitos relacionados ao RabbitMQ e sua arquitetura são:
   - Filas
   - Exchanges
   - Bindings
   - Routing Keys
  - Fila
    - A fila é um armazenamento temporário para mensagens que ainda não foram processadas.
    - As mensagens são publicadas para os Exchanges, que então as redirecionam para a fila correspondente
    - Os consumidores recebem mensagens das filas, processando as suas informações.
    - Ao criar uma fila no RabbitMQ, há várias propriedades importantes que pdoem ser definidas. Entre elas, as principais são:
      - Durabilidade: Se for true, significa que elas sobreviverão a um reinicio do servidor RabbitMQ e as mensagens não confirmadas serão re-enfileiradas
      - Exclusividade: Se for true, significa que a fila será exclusiva, sendo usada por apenas conexão e então excluída quando essa conexão for fechada.
      - Auto-delete: Se for true, ela será automaticamente apagada quando o ultimo consumidor se desconectar.
      - Message TTL: Se refere ao periodo de tempo que uma mensagem não entregue permanece na fila antes de ser descartada ou movida para outra fila. O valor é especificado em milissegundos.
  - Exchange
    - Exchanges são um componente essencial na arquitetura do RabbitMQ
    - Eles recebem mensagems dos produtores e as direcionam para as filas
    - Este direcionamento é baseado em regras denominadas bindings, que são estabelecidas entre as exchanges e as filas
    - Os bindings podem avaliar a Routing Key, que seria um atributo adicionado ao cabeçalho da mensagem, que serve como um endereço que o exchange poderá decidir com rotear a mensagem ao definir o binding
    - Existem 4 tipos de exchange:
      - Direct
      - Default
      - Topic
      - Fanout
    - Direct
      - Envia mensagens para uma ou mais fila(s) que os bindings exatamente encaixa com a routing key
    - Topic
      - Similar ao Direct, mas oferece bem mais flexibilidade pois permite utilizar padrões de correspondecia com o astericos(*) e cerquilha (#), não necessitando ter a binding key igual a routing key
      - Asterisco represennta uma única palavra qualquer
      - Cerquilha representa qualquer numero de palavras
    - Default
      - É uma exchange de tipo "Direct", sem nome "", que todas filas criadas se registram com a routing key igual ao seu nome.
    - Fanout
      - Copia e roteia todas as mensagens recebidadas para todas filas que estão registradas na Exchange, independente de routing keys ou padrões definidos
      
### Comparativos entre ferramentas
 - RabbitMQ é apenas uma das muitas opções disponiveis de ferramentas para mensageria
 - Outras soluções incluem:
   - Apache Kafla
   - ActiveMQ
   - Amazon SQS
   - Azure Service Bus
 - O Apache Kafka, por exemplo, é conhecido por sua alta capacidade de taxa de transferência e capacidade de armazenar grandes volumes de dados
 - Isso o torna particularmente adequado para processamento de dados em tempo real.
 - Ele também é altamente extensivel e integrável com outros serviços, principalmente através de seus conectores
 - No entanto, ele é mais complexo para configurar e gerenciar do que o RabbitMQ
 - Já o ActiveMQ é outra opção open-source que oferece suporte para vários protocolos de mensagens
 - Ele tem uma longa historico de uso em aplicações enterprise e oferece muitos recursos avançados
 - Porém, ele não tem a mesma performance do RabbitMQ ou do Apache Kafka quando se trata de ligar com altas cargas de mensagens
 - O Amazon Simple Queue Service (SQS) é um serviço de fila de mensagens totalmente gerenciado que se integra bem ao ecossistema AWS
 - Ele oferece duas opções principais: filas padrão, que oferecem throughput maximo, e filas FIFO, que preservam a ordem das mensagens.
 - O SQS é simples de configurar e escala facilmente para lidar com altos volumes de mensagens
 - No entanto, em comparação com o RabbitMQ, o SQS é menos flexivel em termos de padrões de roteamento de mensagens. 
 - O Azure Service Bus é a solução de mensageria da Microsoft para a sua plataforma em nuvem, Azure.
 - Oferece recursos como filas, tópicos e assinaturas, e suporta uma variedade de padrões de comunicação, incluindo publish/subscribe,request/reply e peer-to-peer.
 - Assim como o SQS, o Azure Service Bus é totalmente gerenciado e se integra bem ao ecossistema Azure
 - No entanto, pode ser mais caro do que o RabbitMQ ou a SQS, dependendo do volume de mensagens.

### Instalando o RabbitMQ
 - Existem várias maneiras de instalar o RabbitMQ, e que vou abordar aqui:
   - Instalação Manual
   - Instalação com Gerenciadores de Pacotes
   - Usando Docker
   - Serviços em Nuvem
 - Existem várias maneiras de instalar o RabbitMQ, e que vou abordar aqui:
   - Instalação Manual
     - Você pode baixar o RabbitMQ do site oficial e instalá-lo manualmente no seu sistema operacional.
     - Baixar o Erlang, no instalador do RabbitMQ pedi para baixar o Erlang.
     - Baixar o Executável do RabbitMQ
     - CMD: telnet 127.0.0.1 5672
     - CMD: C:\Program Files\RabbitMQ Server\rabbitmq_server-4.1.4\sbin > rabbitmq-plugins enable rabbitmq_management
     - No navegador 127.0.0.1:5672 ou localhost:5672
     - login guest e guest
   - Instalação com Gerenciadores de Pacotes:
     - No windows, dá para usar o Chocolatey. Já no Linux, você pode usar gerenciadores de pacotes como o apt e yum. Para o MacOS, você pode usar o brew
   - Usando Docker:
     - é possivel executar o RabbitMQ em qualquer maquina com suporte a containers Docker, incluindo Windows, MacOS e Linux
     - docker run -d --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3-management
   - Serviços em Nuvem: 
     - você também pode usar um serviço de nuvem que forneça o RabbitMQ como um serviço, como o CloudAMQP.

 ### Conhecendo o RabbitMQ.Client
  - O RabbitMQ é a biblioteca oficial em .NET para RabbitMQ, mantida pela equipe da própria ferramenta.
  - Seu principal beneficio é que fornece controle completo sobre o RabbitMQ, oferecendo acesso direto a todos os recursos do RabbitMQ sem qualquer abstração.
  - Principais Recursos
    - Controle completo
    - Performance
    - Suporte para todos os protocolos RabbitMQ
    - Manutenção pela equipe do RabbitMQ
  - Principais Recursos
    - Controle Completo: Com o RabbitMQ.Client, você tem acesso total a todos os recursos do RabbitMQ, sem as abstações que podem limitar sua flexibilidade.
    - Performance: Como uma biblioteca de baixo nivel, RabbitMQ.Client tende a oferecer melhor desempenho do que bibliotecas de mais alto nivel como EasyNetQ
      - Inclusive, esse é um ponto a se avaliar em comparativos de  todo tipo de ferramenta! Bibliotecas de baixo nivel tendem a terem melhor performance do que bibliotecas          de mais alto nivel, que ofereçam grandes abstações.
    - Suporte para todos os protocolos RabbitMQ: RabbotMQ.Client suporta todos os protocolos RabbitMQ, incluindo AMQP o-9-1, AMQP 1.0 e MQTT
    - Manutenção pela equipe: RabbitMQ.Client é mantida pela mesma equipe que mantem o RabbitMQ, o que garante uma boa compatibilidade e suporte

### Conhecendo o EasyNetQ
 - O EasyNetQ é uma biblioteca open-source para o RabbitMQ
 - A principal característica do EasyNetQ é a simplificação da interação com o RabbitMQ, fornecendo uma interface de alto nível e fácil de usar
 - Com isso , ele esconde muitos dos detalhes de implementação que podem tornar o RabbitMQ dificil de gerenciar
 - Principais recursos
   - Interface de alto nível
   - Serialização/Deserialização de mensagens
   - Reconexão de consumidor
   - Gerenciamento de erros
