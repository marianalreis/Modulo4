# Projeto: Controle de LEDs com Botão (POO + Arduino, sem protoboard)

Projeto desenvolvido no simulador Wokwi utilizando Programação Orientada a Objetos (P.O.O.).  
O circuito utiliza **2 LEDs** (verde e vermelho) controlados por um **botão** conectado diretamente ao **Arduino Uno**, sem protoboard e sem resistores externos de pull-down — aproveitando o **resistor interno (INPUT_PULLUP)**.  

Quando o botão é pressionado, o **LED vermelho** acende e o **LED verde** apaga.  
Quando o botão é solto, o **LED verde** acende e o **LED vermelho** apaga.  
O **Monitor Serial** exibe a mensagem “Botao pressionado!” apenas uma vez por clique.


##  Componentes utilizados
- 1× Arduino Uno  
- 2× LEDs (vermelho e verde)  
- 2× resistores de 220 Ω (limitação de corrente dos LEDs)  
- 1× botão (push button)  
- Fios de conexão  



##  Ligações elétricas (sem protoboard)
- **Pino 2 → LED vermelho → resistor 220 Ω → GND**  
- **Pino 3 → LED verde → resistor 220 Ω → GND**  
- **Pino 4 → botão → GND**  
- Todos os GNDs podem ser ligados ao mesmo pino GND do Arduino  

-

##  Código (POO + INPUT_PULLUP)

```cpp
class Led {
  int pino;
public:
  Led(int p) : pino(p) { pinMode(pino, OUTPUT); }
  void ligar()   { digitalWrite(pino, HIGH); }
  void desligar(){ digitalWrite(pino, LOW);  }
};

class Botao {
  int pino;
public:
  Botao(int p) : pino(p) { pinMode(pino, INPUT_PULLUP); } // resistor interno
  bool pressionado() { return digitalRead(pino) == LOW; } // LOW = apertado
};

Led ledVermelho(2);
Led ledVerde(3);
Botao botao(4);

bool jaImprimiu = false;

void setup() {
  Serial.begin(9600);
}

void loop() {
  bool estado = botao.pressionado();

  if (estado) {
    ledVermelho.ligar();
    ledVerde.desligar();
  } else {
    ledVermelho.desligar();
    ledVerde.ligar();
  }

  if (estado && !jaImprimiu) {
    Serial.println("Botao pressionado!");
    jaImprimiu = true;
    delay(30);
  }

  if (!estado && jaImprimiu) {
    jaImprimiu = false;
    delay(30);
  }
}
```
[Acesse o projeto no Wokwi clicando aqui](https://wokwi.com/projects/445540139118737409)

