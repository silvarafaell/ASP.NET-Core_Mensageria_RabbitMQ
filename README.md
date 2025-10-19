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
      
