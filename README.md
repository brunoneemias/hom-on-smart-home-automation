# 🏠 Smart Home Automation

Projeto de **automação residencial (Smart Home)** desenvolvido durante o curso técnico na ETEC, com integração entre **software e hardware** para simular o controle de dispositivos de uma residência inteligente.

O sistema permite controlar ambientes da casa por meio de uma aplicação com interface gráfica conectada via **Bluetooth** a um **Arduino**, responsável por acionar sensores e dispositivos físicos.

---

##  Interface do Sistema

A interface do aplicativo permite selecionar ambientes da casa e controlar dispositivos conectados.

- Cozinha
- Sala
- Dormitório
- Banheiro
- Garagem

A comunicação com o Arduino é realizada via **Bluetooth**, permitindo enviar comandos e receber respostas do sistema.

---

## ⚙️ Tecnologias Utilizadas

### Software

- **Android Studio** – Desenvolvimento do aplicativo mobile
- **Delphi** – Interface de controle e comunicação
- **Bluetooth Communication** – Conexão entre aplicação e Arduino

### Hardware

- **Arduino**
- **Módulo Bluetooth**
- **Servo Motor**
- **LEDs (controle de iluminação)**
- **Sensor Laser para detecção**
- **Caixa de som para simulação de eventos**

---

## 🔌 Arquitetura do Projeto

O sistema funciona em três camadas principais:

1. **Interface do usuário**
   - Aplicação com layout gráfico para controle da casa

2. **Comunicação**
   - Conexão Bluetooth entre aplicativo e Arduino

3. **Controle físico**
   - Arduino recebe comandos e aciona os dispositivos eletrônicos

Fluxo básico:
- Aplicação → Bluetooth → Arduino → Dispositivos (LEDs, Servo Motor, Sensores) 

---

## 🧠 Funcionalidades

- Controle de iluminação dos ambientes
- Simulação de presença na residência
- Acionamento de dispositivos via Bluetooth
- Monitoramento básico de sensores
- Interface visual para seleção de ambientes

---

## 🛠️ Estrutura do Projeto
smart-home-automation
│
├── mobile-app
├── arduino-code
├── bluetooth-control
├── audio-system
└── interface-delphi


---

## 🎯 Objetivo do Projeto

Explorar conceitos de:

- Automação residencial
- Internet das Coisas (IoT)
- Integração entre hardware e software
- Comunicação Bluetooth
- Controle de dispositivos embarcados

---

## 👨‍💻 Autor

**Bruno Neemias**

📎 GitHub  
https://github.com/brunoneemias

---

## 📚 Observação

Este projeto foi desenvolvido para fins educacionais como parte das atividades do curso técnico na **ETEC**, com o objetivo de aplicar conceitos de automação e integração de sistemas.
