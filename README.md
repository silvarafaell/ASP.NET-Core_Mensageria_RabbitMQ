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
