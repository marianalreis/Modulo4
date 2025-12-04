
# Resolução lista de exercício - 4° módulo

1. **E)** Absorver flutuações de tensão: liberando energia instantaneamente quando há uma queda rápida (pico de consumo) e guardando energia quando há um aumento súbito (pico de tensão).
2. **E)** Modelar uma entidade do mundo real, focando nas propriedades (atributos) e nos comportamentos (métodos) essenciais para a representação, ignorando detalhes irrelevantes.
3. **D)** Quanto maior o número de bits do ADC (como de 8 para 12), maior é a sensibilidade e menor é o valor de tensão correspondente a cada nível, permitindo que o microcontrolador enxergue o sinal mais finamente.
4. **D)** RNF B é superior porque é mensurável, substituindo a vagueza do termo "rápido" por uma métrica objetiva de tempo (< 1 s).
5. **D)** MQTT, CoAP e AMQP.
6. **C)** 75% de Duty Cycle. Isso simula uma tensão analógica equivalente a 75% da tensão total, resultando em menor energia média, menor torque e menor velocidade no motor.
7. **B)** Proteger os atributos internos (dados / estado) da classe com o uso de modificadores de acesso (private) e limitar a interação externa a métodos controlados (getters/setters), impedindo o acesso direto aos atributos.
8. **B)** Permitir que a função acesse diretamente o endereço de memória da variável original e modifique seu valor real, sendo útil para leituras de sensores, buffers ou passagem de estruturas grandes sem gastar memória extra com cópias.
9. **E)** O Regulador de tensão AMS1117.
10. **B)** Esses pinos são usados pelo chip para definir o modo de inicialização, e a mudança automática de estado pode ligar relés sozinhos ou enviar comandos errados a sensores no momento do boot.
11. **C)** Ele precisa estar conectado e se comunicar com outros dispositivos, sistemas ou com a Internet, pois, sem essa conexão, é considerado apenas um dispositivo eletrônico comum.
12. **B)** Se o componente "muda o mundo" (modifica fisicamente o ambiente) ou se ele "mostra o mundo" (apenas apresenta informações sobre o estado do sistema para o usuário).
13. **D)** O Erro de Quantização é considerado inevitável, pois toda conversão digital envolve um arredondamento do valor real do sinal analógico para o nível discreto mais próximo.
14. **C)** Evitar o uso dos pinos do bloco ADC2 (GPIOs 0, 2, 4, 12–15, 25–27), pois eles entram em conflito quando o Wi-Fi está ativo.
15. **D)** O requisito 2 é superior por associar o RNF (latência) a um contexto funcional do projeto (envio de dados MQTT), tornando-o mais claro e facilitando a validação.
16. **C)** TCP (Transmission Control Protocol) e UDP (User Datagram Protocol).
17. **E)** MQTT e AMQP.
18. **C)** Botões e Sensores (que devolvem leituras de luminosidade, temperatura ou outros sinais que necessitam de leitura/medição).
19. **C)** Sensores Resistivos, Capacitivos, Indutivos, Piezoelétricos e Termoelétricos/Fotoelétricos.
20. **E)** Ele atende à Mensurabilidade, utilizando uma métrica objetiva (mA), e pode ser validado por meio de Testes de Consumo (usando um multímetro/medidor USB).
21. **A)** O motor vibra muito rápido, mas mantém o torque e a velocidade máximos.
22. **D)** O ESP32 apenas energiza a bobina de baixa potência do relé, que cria um campo magnético; esse campo, por sua vez, puxa um contato mecânico para fechar o circuito da carga (atuador), permitindo que a alta potência de uma fonte externa flua, sem contato físico com o microcontrolador.
23. **D)** Ele deve ser colocado em paralelo com o componente (entre VCC e GND), o mais próximo possível, para liberar energia instantaneamente em quedas de tensão (picos de consumo) e absorver energia em aumentos súbitos (ruído).
24. **D)** O array é um bloco fixo de memória cujo nome é um ponteiro estático que não pode mudar de endereço, enquanto o ponteiro é uma variável que pode ser reatribuída para apontar para diferentes lugares na memória.
25. **D)** O transmissor utiliza um oscilador de alta frequência (GHz) para fazer elétrons vibrarem rapidamente, gerando ondas eletromagnéticas. O circuito modulador "pinta" essas ondas para que elas carreguem os dados (bits).
