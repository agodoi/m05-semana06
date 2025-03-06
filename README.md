# Atendimento do Professor

## Terças e quintas. Professor de horário parcial. Nesses 2 dias, podem contar comigo!

# Semama 06 - Polarização do Transistor

## Impactos no seu Projeto

### Circuitos Extras Utilizando o **Transistor BC548** para os Periféricos do Robô


#### 1. Circuito de Detecção de Objeto Manipulado
- **Descrição:** Um sensor de fim de curso ou um interruptor reed pode ser conectado ao braço manipulador do robô. Quando um objeto for coletado, o contato é fechado e um sinal pode ser enviado ao Raspberry Pi Pico.
- **Uso do BC548:** O transistor pode ser utilizado como um **amplificador de sinal** ou como um **interruptor eletrônico**, garantindo que o sinal do sensor seja adequadamente processado.
- **Exemplo de circuito:**
  - Entrada do sensor conectada à base do BC548 com potenciômetro de limitação de modo a liberar 3,3V na entrada do microcontrolador.
  - Coletor conectado à alimentação e emissor ao GPIO do Raspberry Pi Pico.
  - Quando o sensor fechar o circuito, o transistor satura e ativa a entrada do microcontrolador, liberando 3,3V.

---

#### 2. Circuito de Ativação do Leitor de Código de Barras
- **Descrição:** Para economizar energia, o leitor de código de barras pode ser ativado apenas quando necessário, evitando consumo excessivo.
- **Uso do BC548:** Funcionando como **chave eletrônica**, o BC548 pode ser acionado por um pulso do GPIO do Raspberry Pi Pico para ligar/desligar o módulo do leitor.
- **Exemplo de circuito:**
  - Base do BC548 conectada ao GPIO do Raspberry Pi Pico via resistor.
  - Coletor conectado ao positivo do leitor de código de barras.
  - Emissor conectado ao GND.
  - Quando o GPIO for ativado, o transistor liga o leitor.

---

### 3. Indicador Visual de Estado (LED de Status)
- **Descrição:** LEDs podem ser usados para indicar estados operacionais dos periféricos (exemplo: objeto detectado, leitor ativo, erro, etc.).
- **Uso do BC548:** Controle de corrente para acionamento de LEDs de alta intensidade sem sobrecarregar as saídas do microcontrolador.
- **Exemplo de circuito:**
  - Base do BC548 conectada a um GPIO do Raspberry via resistor (1kΩ).
  - Coletor conectado ao LED e ao resistor limitador de corrente.
  - Emissor ao GND.
  - Quando o GPIO for ativado, o LED acende.

---

### 4. Driver de Relé para Acionamento de Componentes Externos
- **Descrição:** O Raspberry Pi Pico pode não fornecer corrente suficiente para acionar relés diretamente. Um circuito com o BC548 pode permitir o controle de relés para ligar/desligar atuadores mecânicos do robô.
- **Uso do BC548:** O transistor pode funcionar como **driver de relé**, permitindo que uma corrente mais alta passe pelo relé sem sobrecarregar o microcontrolador.
- **Exemplo de circuito:**
  - Base conectada ao GPIO do Raspberry via resistor (1kΩ).
  - Coletor ligado ao relé e à alimentação.
  - Emissor ao GND.
  - Diodo de proteção em paralelo ao relé.

---

### 5. Amplificação de Sinal de Sensores de Baixa Potência
- **Descrição:** Caso algum sensor de proximidade ou fototransistor forneça um sinal muito fraco, o BC548 pode amplificar esse sinal antes de enviá-lo ao Raspberry Pi Pico.
- **Uso do BC548:** Como amplificador de tensão ou corrente para sensores que operam com variação mínima de sinal.

---

### 6. Circuito de Alerta Sonoro (Buzzer)
- **Descrição:** Caso seja necessário alertar quando um objeto for coletado, um **buzzer piezoelétrico** pode ser acionado pelo Raspberry Pi Pico com a ajuda do BC548.
- **Uso do BC548:** O transistor pode atuar como chave para permitir a corrente suficiente ao buzzer.
- **Exemplo de circuito:**
  - Base do BC548 conectada ao GPIO via resistor (1kΩ).
  - Coletor conectado ao buzzer e à alimentação.
  - Emissor ao GND.
  - Quando o GPIO for ativado, o buzzer emite som.

---

### Resumo
O **BC548** é um transistor versátil que pode ser usado para:
- **Controle de sensores** (detecção de objeto, leitor de código de barras).
- **Ativação de periféricos** (acionamento de relés, buzzers, LEDs).
- **Amplificação de sinais** (de sensores fracos para entrada do microcontrolador).


# Funcionamento do Transistor

<img src="https://github.com/agodoi/m05-semana06/blob/main/imgs/transistor.jpeg" width="600">


<img src="https://github.com/agodoi/m05-semana06/blob/main/imgs/transistor-bc548-pinagem.jpg" width="300">
<img src="https://github.com/agodoi/m05-semana06/blob/main/imgs/transistor-tip41.png" width="300">
