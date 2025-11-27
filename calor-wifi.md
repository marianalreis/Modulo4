# 📡 Monitoramento de Sinal Wi-Fi com ESP32 (MQTT + Adafruit IO)

Projeto que utiliza um **ESP32** para medir continuamente a intensidade do sinal Wi-Fi (em dBm) e enviar os dados para a plataforma **Adafruit IO** via protocolo **MQTT**, exibindo tudo em um **dashboard em tempo real**.

---

## 🔧 Objetivo

* Ler o nível do sinal Wi-Fi usando `WiFi.RSSI()`.
* Enviar os dados para o feed **wifi-signal** no Adafruit IO.
* Criar um dashboard online com gráfico em tempo real.

---

## 🛠️ Componentes Utilizados

| Quantidade | Componente           |
| ---------- | -------------------- |
| 1          | ESP32 DevKit V1      |
| 1          | Cabo micro-USB       |
| —          | Wi-Fi 2.4 GHz        |
| —          | Conta no Adafruit IO |

---

## 🧩 Arquitetura

```
ESP32
   ↓ Wi-Fi
MQTT (porta 1883)
   ↓
Adafruit IO Feed
   ↓
Dashboard (gráfico)
```

---

## 🔑 Pré-requisitos

### 1) No Adafruit IO

* Criar conta em: [https://io.adafruit.com](https://io.adafruit.com)
* Criar feed: **wifi-signal**
* Criar dashboard e adicionar o feed
* Obter:

  * **AIO_USERNAME**
  * **AIO_KEY**
    (Menu → Account → View AIO Key)

### 2) No Arduino IDE

Instalar:

* Placas ESP32
* Biblioteca **PubSubClient**
* Biblioteca **Adafruit MQTT** (opcional)

---

## 💻 Código Utilizado

```cpp
#include <WiFi.h>
#include <PubSubClient.h>

#define WIFI_SSID   "Mari"
#define WIFI_PASS   "Belinha0101"

#define AIO_USERNAME "marianareis"
#define AIO_KEY      "aio_xxxxxxxxxxxxxxxxxxxxx"
#define FEED_KEY     "wifi-signal"

const char* MQTT_BROKER = "io.adafruit.com";
const int   MQTT_PORT   = 1883;

WiFiClient espClient;
PubSubClient client(espClient);

char mqttTopic[100];

void conectaWiFi() {
  Serial.print("Conectando ao WiFi: ");
  Serial.println(WIFI_SSID);

  WiFi.begin(WIFI_SSID, WIFI_PASS);

  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("WiFi conectado!");
}

void conectaMQTT() {
  sprintf(mqttTopic, "%s/feeds/%s", AIO_USERNAME, FEED_KEY);

  while (!client.connected()) {
    Serial.println("Conectando ao MQTT...");
    if (client.connect("ESP32", AIO_USERNAME, AIO_KEY)) {
      Serial.println("MQTT conectado!");
    } else {
      Serial.print("Erro: ");
      Serial.println(client.state());
      delay(2000);
    }
  }
}

void setup() {
  Serial.begin(115200);
  conectaWiFi();
  client.setServer(MQTT_BROKER, MQTT_PORT);
  conectaMQTT();
}

void loop() {
  if (!client.connected()) conectaMQTT();

  int dBm = WiFi.RSSI();
  char payload[10];
  sprintf(payload, "%d", dBm);

  client.publish(mqttTopic, payload);
  Serial.printf("dBm: %d (ENVIADO)\n", dBm);

  delay(2000);
}
```

---

## 📊 Resultado Esperado

O dashboard exibirá:

* Valores atualizados a cada 2 segundos
* Gráfico em tempo real
* Histórico de intensidade do sinal (dBm)

---

## 🎬 Vídeo de Demonstração

[Clique aqui para acessar](https://drive.google.com/file/d/17PA_Uml7PQSC1Yq-cV_VISTBI5hcQRB3/view?usp=sharing)


---

## 👤 Autoria

**Mariana Lacerda Reis**
