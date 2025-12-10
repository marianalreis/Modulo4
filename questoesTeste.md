

# **1) Análise da falha no sistema**

Ao analisar a imagem da montagem junto com o código, dá para perceber que o sistema parou de funcionar principalmente porque a entrada do botão não existe fisicamente. O código depende do `digitalRead(7)` para iniciar toda a lógica do semáforo, mas na protoboard não há nada ligado ao pino 7; inclusive, onde deveria estar o botão, foi colocado um LED. Como não existe nenhuma entrada real para acionar o ciclo, a condição do `if` nunca se torna verdadeira e o semáforo não executa nenhuma das transições.

Além disso, observando a montagem, alguns LEDs estão ligados de forma incorreta, com trilhas onde 5V e GND aparecem na mesma linha, o que pode impedir o LED de acender ou até gerar curto. A polaridade também parece estar invertida em alguns pontos, e o caminho correto (**ânodo → resistor → pino digital / cátodo → GND**) não está sendo seguido. Isso faz com que os LEDs não respondam aos comandos dos pinos que o código controla.

O código ainda apresenta alguns erros de sintaxe, como `pin Mode` no lugar de `pinMode` e um `delay` sem ponto e vírgula, o que já impediria a compilação antes mesmo de testar o circuito. Somando tudo isso — a entrada inexistente, a polaridade errada dos LEDs, trilhas incorretas e problemas de sintaxe — o sistema realmente não teria como funcionar. Para corrigir, seria preciso reinstalar o botão no pino 7, ajustar a polaridade e trilhas dos LEDs, garantir que cada um esteja ligado ao pino correspondente do código e corrigir os comandos escritos de forma incorreta.

---

# **2) Explicação do funcionamento do código orientado a objetos**

No código apresentado, a ideia é organizar o funcionamento dos semáforos usando classes. A primeira classe, chamada `Signal`, funciona como um “modelo geral” de qualquer semáforo, porque ela guarda quais são os pinos do vermelho, do amarelo e do verde, e já traz métodos prontos para acender cada cor. Então, qualquer tipo de semáforo que for criado depois já começa com essas funções básicas prontas.

A partir desse modelo geral, são criadas duas versões específicas: uma para carros (`CarSignal`) e outra para pedestres (`PedSignal`). Como elas herdam tudo da classe `Signal`, não precisam repetir o código para acender cada luz; apenas acrescentam o que é exclusivo de cada tipo. Por exemplo, o semáforo de carros tem um método para preparar a parada, acendendo o amarelo por um tempo. Já o de pedestres tem métodos simples para liberar ou impedir a travessia, acendendo o verde ou vermelho.

Depois existe a classe `TrafficController`, que é quem realmente coordena tudo. Ela recebe os dois semáforos e controla a lógica do sistema: quando o botão é pressionado, ela faz o semáforo de carros passar do verde para o amarelo e depois para o vermelho, libera os pedestres, espera o tempo de travessia e depois volta tudo ao estado inicial. O detalhe é que o controlador usa ponteiros para a classe base (`Signal`), o que permite tratar os dois tipos de semáforo de forma parecida, mesmo eles sendo diferentes. Isso é o uso de **polimorfismo**, mas de modo simples: ele só chama os métodos e cada semáforo responde do jeito certo.

No final, todo esse arranjo serve para organizar melhor o código: a classe base define o que é comum, as classes filhas adicionam o que é específico, e o controlador faz tudo funcionar como um sistema real de semáforo.
