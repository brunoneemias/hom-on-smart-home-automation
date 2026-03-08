# 💡 Sistema de Iluminação Automatizada com Arduino

> Módulo de controle de iluminação do projeto **Smart Home**, desenvolvido com Arduino, Bluetooth e sensores de luminosidade.

---

## 📖 Sobre o Projeto

Este módulo faz parte de um sistema maior de **automação residencial (Smart Home)** e é responsável pelo controle inteligente da iluminação da casa. Utilizando **Arduino**, **Bluetooth (HC-05)** e um **sensor LDR**, o sistema permite acionar as luzes de diferentes ambientes via aplicativo, além de automatizar a iluminação externa com base na luminosidade do ambiente.

Desenvolvido para fins educacionais, o projeto explora conceitos de programação embarcada, comunicação sem fio e integração entre software e hardware.

---

## 🎯 Objetivos

- Controle manual das luzes por Bluetooth via aplicativo
- Acionamento de ambientes específicos da residência
- Automação da iluminação externa com base na luminosidade (LDR)
- Integração entre software embarcado e hardware físico

---

## 🛠️ Tecnologias e Componentes

### Software
| Ferramenta | Descrição |
|---|---|
| Arduino IDE | Ambiente de desenvolvimento |
| C / C++ | Linguagem de programação |
| SoftwareSerial | Biblioteca para comunicação Bluetooth |

### Hardware
| Componente | Quantidade |
|---|---|
| Arduino (Uno ou compatível) | 1 |
| Módulo Bluetooth HC-05 | 1 |
| LDR (sensor de luminosidade) | 1 |
| LEDs | 10 |
| Resistores | conforme necessário |
| Protoboard e jumpers | — |

---

## 🏠 Mapeamento da Iluminação

O sistema controla **10 pontos de iluminação**, cada um mapeado a um ambiente da residência:

| Ambiente | Índice | Pino Arduino |
|---|:---:|:---:|
| Sala | 0 | 12 |
| Cozinha | 1 | 13 |
| Banheiro 1 | 2 | 2 |
| Garagem | 3 | 3 |
| Atrás da Garagem | 4 | 4 |
| Quarto 1 | 5 | 5 |
| Quarto 2 | 6 | 6 |
| Quarto 3 | 7 | 7 |
| Banheiro 2 | 8 | 8 |
| Porta e Varanda | 9 | 9 |

---

## 🔵 Comunicação Bluetooth

A comunicação é realizada via módulo **HC-05** com a biblioteca `SoftwareSerial`.

**Pinagem:**
- RX do HC-05 → pino **10** do Arduino  
- TX do HC-05 → pino **11** do Arduino

```cpp
#include <SoftwareSerial.h>
SoftwareSerial HC05(10, 11);
```

Os comandos são enviados pelo aplicativo e interpretados pelo Arduino para ligar ou desligar os LEDs correspondentes a cada ambiente.

---

## 🌙 Automação com LDR

O sensor **LDR** está conectado na porta analógica **A5** e mede continuamente a luminosidade do ambiente.

**Comportamento:**
- 🌑 Ambiente **escuro** → iluminação externa acionada automaticamente  
- ☀️ Ambiente **claro** → iluminação externa desligada automaticamente

Áreas controladas pela automação:
- Porta e Varanda (pino 9)
- Banheiro 2 / área externa (pino 8)

---

## 🧠 Lógica do Programa

```
Inicialização
├── Inicia comunicação serial
├── Inicia comunicação Bluetooth (HC-05)
├── Configura pinos como OUTPUT
└── Realiza teste sequencial em todos os LEDs

Loop principal
├── Lê valor do LDR
│   ├── Escuro → liga iluminação externa
│   └── Claro  → desliga iluminação externa
└── Verifica comandos Bluetooth
    ├── Recebe índice do ambiente
    └── Liga / desliga o LED correspondente
```

---

## 💻 Código Principal

```cpp
#include <SoftwareSerial.h>
SoftwareSerial HC05(10, 11);

int Luzes[10] = {12, 13, 2, 3, 4, 5, 6, 7, 8, 9};
int comando = 0;
int LDR = A5;

void setup() {
  Serial.begin(9600);
  HC05.begin(38400);

  // Configura pinos e realiza teste inicial
  for (int nP = 0; nP < 10; nP++) {
    pinMode(Luzes[nP], OUTPUT);
    digitalWrite(Luzes[nP], HIGH);
    delay(500);
    digitalWrite(Luzes[nP], LOW);
  }

  Serial.println("Setup finalizado!");
}
```

---

## ✅ Funcionalidades Implementadas

- [x] Teste automático sequencial dos LEDs na inicialização
- [x] Controle de até 10 pontos de iluminação
- [x] Comunicação Bluetooth com aplicativo mobile
- [x] Leitura de luminosidade via LDR
- [x] Automação da iluminação externa

--

## 📚 Conceitos Aplicados

- Programação embarcada (C/C++ no Arduino)
- Vetores e arrays
- Comunicação serial e Bluetooth
- Leitura de sensores analógicos
- Automação residencial
- Integração software-hardware

---

## 🚀 Melhorias Futuras

- [ ] Comandos individuais ON/OFF por ambiente via app
- [ ] Feedback do estado atual de cada luz
- [ ] Monitoramento em tempo real via serial/app
- [ ] Controle por Wi-Fi com ESP8266/ESP32 (IoT)
- [ ] Integração com mais sensores (presença, temperatura)
- [ ] Dashboard de controle web ou mobile

---

## 👨‍💻 Autor

**Bruno Neemias**  
Projeto desenvolvido para fins educacionais, como parte de estudos em automação residencial e sistemas embarcados.

[![GitHub](https://img.shields.io/badge/GitHub-brunoneemias-181717?style=flat&logo=github)](https://github.com/brunoneemias)

---

## 📌 Observação

Este repositório representa o **módulo de iluminação** de um projeto maior de Smart Home, no qual diferentes dispositivos físicos são controlados por software com apoio de Arduino e comunicação sem fio. Outros módulos do sistema podem incluir controle de motores, sensores de presença e integração com automação de persianas ou portões.
