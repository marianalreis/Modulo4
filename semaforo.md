# 🚦 Projeto Semáforo com Arduino

## 📘 Descrição
Este projeto tem como objetivo simular o funcionamento de um **semáforo de trânsito** utilizando o **Arduino UNO**, **LEDs** e **resistores**.  

---

## 🧩 Materiais Utilizados

| Componente | Quantidade | Descrição |
|-------------|-------------|-----------|
| Arduino UNO | 1 | Placa de controle do circuito |
| LED Vermelho | 1 | Representa o sinal de "Pare" |
| LED Amarelo | 1 | Representa o sinal de "Atenção" |
| LED Verde | 1 | Representa o sinal de "Siga" |
| Resistores 220 Ω | 3 | Limitam a corrente dos LEDs |
| Protoboard | 1 | Placa para montagem sem solda |
| Jumpers | 10 | Fios de conexão |
| Cabo USB | 1 | Conexão com o computador para programação |

---

## ⚙️ Montagem do Circuito

Os LEDs foram dispostos verticalmente na protoboard (vermelho, amarelo e verde).  
Cada LED está conectado em **série com um resistor de 220 Ω**.

### 🧠 Ligações dos pinos:

| Cor do LED | Pino do Arduino | Ligação |
|-------------|----------------|----------|
| Vermelho | 13 | LED → resistor → pino 13 |
| Amarelo | 12 | LED → resistor → pino 12 |
| Verde | 11 | LED → resistor → pino 11 |
| Todos os negativos | GND | Linha azul da protoboard conectada ao GND do Arduino |

---

## 💻 Código Utilizado

```cpp

class Semaforo {
  private:
    int* leds[3]; 
  public:
   
    Semaforo(int* pVermelho, int* pAmarelo, int* pVerde) {
      leds[0] = pVermelho;
      leds[1] = pAmarelo;
      leds[2] = pVerde;
    }

  
    void iniciar() {
      pinMode(*leds[0], OUTPUT);
      pinMode(*leds[1], OUTPUT);
      pinMode(*leds[2], OUTPUT);
    }

  
    void vermelho() {
      digitalWrite(*leds[0], HIGH);
      digitalWrite(*leds[1], LOW);
      digitalWrite(*leds[2], LOW);
      delay(6000);
    }

    void verde() {
      digitalWrite(*leds[0], LOW);
      digitalWrite(*leds[1], LOW);
      digitalWrite(*leds[2], HIGH);
      delay(4000);
    }

    void amarelo() {
      digitalWrite(*leds[0], LOW);
      digitalWrite(*leds[1], HIGH);
      digitalWrite(*leds[2], LOW);
      delay(2000);
    }
};


int pinoVermelho = 13;
int pinoAmarelo  = 12;
int pinoVerde    = 11;

Semaforo semaforo(&pinoVermelho, &pinoAmarelo, &pinoVerde);

void setup() {
  semaforo.iniciar();
}

void loop() {
  semaforo.vermelho();
  semaforo.amarelo();
  semaforo.verde();
}
```
---
## 🧠 Funcionamento

O código foi programado para seguir o ciclo contínuo de um semáforo real:

Vermelho acende por 6 segundos → veículos param.

Verde acende por 4 segundos → veículos podem seguir.

Amarelo acende por 2 segundos → aviso de mudança.

Após isso, o ciclo se repete indefinidamente.

## 🎥 Demonstração

[Clique aqui para ver o vídeo de funcionamento](https://drive.google.com/file/d/1pTQS-wJDovbb1JTUy3Y4lT6WuL7IIhcl/view?usp=sharing)

O vídeo mostra:

- O circuito funcionando na protoboard;

- A autora demonstrando a montagem e explicando o tempo de cada fase.

- Todos os LEDs possuem resistores de 220 Ω para evitar danos.

- O código foi testado e apresentou a temporização correta (6s / 4s / 2s).

- O circuito foi montado de forma limpa e organizada, garantindo segurança e clareza visual.
