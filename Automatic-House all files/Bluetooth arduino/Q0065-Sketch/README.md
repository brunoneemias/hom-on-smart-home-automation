# 🤖 Arduino — Comunicação Bluetooth

> Módulo de comunicação entre o Arduino e o app **hom\<on>** via Bluetooth, responsável por interpretar comandos e acionar os dispositivos da residência.

---

## 📖 Sobre

Este código gerencia a **recepção de comandos Bluetooth** enviados pelo app e os traduz em ações físicas nos pinos do Arduino, ligando ou desligando os dispositivos de cada ambiente.

A comunicação utiliza um **protocolo de byte customizado**, onde cada byte recebido carrega tanto o ambiente alvo quanto a ação a ser executada (ligar/desligar).

---

## 🔌 Pinagem

| Ambiente | Pino Arduino |
|---|:---:|
| Sala | 12 |
| Cozinha | 13 |
| Banheiro 1 | 2 |
| Garagem | 3 |
| Atrás da Garagem | 4 |
| Quarto 1 | 5 |
| Quarto 2 | 6 |
| Quarto 3 | 7 |
| Banheiro 2 | 8 |
| Porta e Varanda | 9 |

Bluetooth HC-05: **RX → pino 10 / TX → pino 11**

---

## 🧠 Protocolo de Comunicação

Cada comando trafega como **1 byte**, com os bits organizados assim:

```
Bit 7 | Bit 6 | Bit 5 | Bits 4~0
  —   | flag  | ação  | número do ambiente (1~10)
```

| Bit | Função |
|:---:|---|
| 6 | Flag de identificação do pacote |
| 5 | Ação — `1` = ligar / `0` = desligar |
| 4~0 | Índice do ambiente (1 a 10) |

### Leitura no Arduino:
```cpp
boolean acao  = bitRead(byteRecebido, 5);  // ligar ou desligar
byte    porta = bitClear(bitClear(byteRecebido, 6), 5); // índice do ambiente
digitalWrite(pinPortas[porta - 1], !acao);
```

---

## 💻 Código Completo

```cpp
#include <SoftwareSerial.h>
SoftwareSerial serial1(10, 11); // RX, TX

int pinPortas[10] = {12, 13, 2, 3, 4, 5, 6, 7, 8, 9};

void setup() {
  serial1.begin(9600);
  for (int nP = 0; nP < 10; nP++) {
    pinMode(pinPortas[nP], OUTPUT);
    byte byteEnviar = nP + 1;
    byteEnviar = bitSet(bitSet(byteEnviar, 6), 5);
    serial1.println(byteEnviar);
  }
}

void loop() {
  if (serial1.available()) {
    byte byteRecebido = serial1.read();
    boolean acao  = bitRead(byteRecebido, 5);
    byte    porta = bitClear(bitClear(byteRecebido, 6), 5);
    digitalWrite(pinPortas[porta - 1], !acao);
  }
}
```

---

## ⚙️ Funcionamento

**Setup:**
- Inicia comunicação Bluetooth a 9600 bps
- Configura todos os pinos como `OUTPUT`
- Envia um byte de identificação para cada ambiente (inicialização do canal)

**Loop:**
- Aguarda bytes chegando via Bluetooth
- Extrai a **ação** (bit 5) e o **ambiente** (bits 0~4) do byte recebido
- Aciona o pino correspondente com `digitalWrite`

---

## 👨‍💻 Autor

**Bruno Neemias** — Projeto educacional desenvolvido na **ETEC**.

[![GitHub](https://img.shields.io/badge/GitHub-brunoneemias-181717?style=flat&logo=github)](https://github.com/brunoneemias)
