# Atendimento do Professor

## Terças e quintas. Professor de horário parcial. Nesses 2 dias, podem contar comigo!

# Semama 06 - Polarização do Transistor

## (1) Impactos no seu Projeto

### Imagine quais circuitos você poderia desenvolver usando um transistor para adicionar no seu projeto. Aqui vão alguns exemplos:

#### 1.1 Circuito de Detecção de Objeto Manipulado
- **Descrição:** Um sensor de fim de curso ou um interruptor reed pode ser conectado ao braço manipulador do robô. Quando um objeto for coletado, o contato é fechado e um sinal pode ser enviado ao Raspberry Pi Pico.
- **Uso do BC548:** O transistor pode ser utilizado como um **amplificador de sinal** ou como um **interruptor eletrônico**, garantindo que o sinal do sensor seja adequadamente processado.
- **Exemplo de circuito:**
  - Entrada do sensor conectada à base do BC548 com potenciômetro de limitação de modo a liberar 3,3V na entrada do microcontrolador.
  - Coletor conectado à alimentação e emissor ao GPIO do Raspberry Pi Pico.
  - Quando o sensor fechar o circuito, o transistor satura e ativa a entrada do microcontrolador, liberando 3,3V.

---

#### 1.2 Circuito de Ativação do Leitor de Código de Barras
- **Descrição:** Para economizar energia, o leitor de código de barras pode ser ativado apenas quando necessário, evitando consumo excessivo.
- **Uso do BC548:** Funcionando como **chave eletrônica**, o BC548 pode ser acionado por um pulso do GPIO do Raspberry Pi Pico para ligar/desligar o módulo do leitor.
- **Exemplo de circuito:**
  - Base do BC548 conectada ao GPIO do Raspberry Pi Pico via resistor.
  - Coletor conectado ao positivo do leitor de código de barras.
  - Emissor conectado ao GND.
  - Quando o GPIO for ativado, o transistor liga o leitor.

---

#### 1.3 Indicador Visual de Estado (LED de Status)
- **Descrição:** LEDs podem ser usados para indicar estados operacionais dos periféricos (exemplo: objeto detectado, leitor ativo, erro, etc.).
- **Uso do BC548:** Controle de corrente para acionamento de LEDs de alta intensidade sem sobrecarregar as saídas do microcontrolador.
- **Exemplo de circuito:**
  - Base do BC548 conectada a um GPIO do Raspberry via resistor (1kΩ).
  - Coletor conectado ao LED e ao resistor limitador de corrente.
  - Emissor ao GND.
  - Quando o GPIO for ativado, o LED acende.

---

#### 1.4 Driver de Relé para Acionamento de Componentes Externos
- **Descrição:** O Raspberry Pi Pico pode não fornecer corrente suficiente para acionar relés diretamente. Um circuito com o BC548 pode permitir o controle de relés para ligar/desligar atuadores mecânicos do robô.
- **Uso do BC548:** O transistor pode funcionar como **driver de relé**, permitindo que uma corrente mais alta passe pelo relé sem sobrecarregar o microcontrolador.
- **Exemplo de circuito:**
  - Base conectada ao GPIO do Raspberry via resistor (1kΩ).
  - Coletor ligado ao relé e à alimentação.
  - Emissor ao GND.
  - Diodo de proteção em paralelo ao relé.

---

#### 1.5 Amplificação de Sinal de Sensores de Baixa Potência
- **Descrição:** Caso algum sensor de proximidade ou fototransistor forneça um sinal muito fraco, o BC548 pode amplificar esse sinal antes de enviá-lo ao Raspberry Pi Pico.
- **Uso do BC548:** Como amplificador de tensão ou corrente para sensores que operam com variação mínima de sinal.

---

#### 1.6 Circuito de Alerta Sonoro (Buzzer)
- **Descrição:** Caso seja necessário alertar quando um objeto for coletado, um **buzzer piezoelétrico** pode ser acionado pelo Raspberry Pi Pico com a ajuda do BC548.
- **Uso do BC548:** O transistor pode atuar como chave para permitir a corrente suficiente ao buzzer.
- **Exemplo de circuito:**
  - Base do BC548 conectada ao GPIO via resistor (1kΩ).
  - Coletor conectado ao buzzer e à alimentação.
  - Emissor ao GND.
  - Quando o GPIO for ativado, o buzzer emite som.

---

#### Resumo
O **BC548** é um transistor versátil que pode ser usado para:
- **Controle de sensores** (detecção de objeto, leitor de código de barras).
- **Ativação de periféricos** (acionamento de relés, buzzers, LEDs).
- **Amplificação de sinais** (de sensores fracos para entrada do microcontrolador).

---
## (2) Transistor

### (2.1) O que é um transistor?

O **transistor** é um **componente eletrônico semicondutor** usado para amplificar ou chavear sinais elétricos. 
Ele é fundamental na eletrônica moderna e está presente em 99% todos os circuitos eletrônicos.


### (2.2) **Estrutura Básica

Um transistor bipolar (como o **BC548** e o **TIP41C**) possui **três terminais**:

I)   **Base (B):** Controla o fluxo de corrente entre C e E.
II)  **Coletor (C):** Entrada principal de corrente.
III) **Emissor (E):** Saída da corrente.

👉 Existem dois tipos principais de transistores bipolares:
- **NPN** (mais comum).
- **PNP**

O **NPN** é o que usaremos como exemplo.

N ➝ Negativo, pino Coletor (C)

P ➝ Positivo, pino Base (B)

N ➝ Negativo, pino Emissor (E)

## 📌 Como o Transistor Funciona?

O transistor funciona como uma **chave eletrônica** ou **amplificador de corrente**.

### 🏷️ 1. Modo "Chave Liga/Desliga" (Saturação e Corte)
- Se **nenhuma corrente** fluir para a **Base (B)** ➝ O transistor fica **desligado** (isto é, **corte**).
- Se **uma pequena corrente em [mA]** fluir para a **Base (B)** ➝ O transistor liga e permite uma **corrente maior em [A]** entre **Coletor (C) e Emissor (E)** (isto é, **saturação**).

**Exemplo prático:**  
Imagine um botão pressão que ativa um motor.
- Quando o botão está solto (**Base sem corrente**), o motor está desligado.
- Quando o botão é pressionado (**Base recebe corrente**), o motor liga.

---

### 🏷️ 2. Modo "Amplificador"
Se aplicarmos uma pequena corrente na **Base**, da ordem de miliampéres, ela **controla** uma corrente muito maior, da ordem de ampéres, do **Coletor para o Emissor**.

💡 **Fórmula básica:**  
```I_C = β * I_B```

Onde:
- \( I_C \) = corrente no **Coletor**
- \( I_B \) = corrente na **Base**
- \( β \) (ou "ganho") = fator de amplificação do transistor

**Exemplo prático:**  
- Um microfone capta um som muito fraco (corrente pequena).
- O transistor amplifica essa corrente e a envia para um alto-falante.
- O som sai alto e audível!

## Resumo:

**(a)** Transistor possui 3 pinos: Coletor (C), Base (B) e Emissor (E). 
**(b)** Existe 2 tipos de transistor: **NPN** e PNP.
**(c)** Todo transistor possui dois modos de trabalho: **Chave Liga-desliga** e Amplificador


## 📌 Exemplo de Circuito Prático
Vamos usar um **LED** controlado por um **transistor NPN (BC548)**.

### 🛠️ **Componentes:**
- **1 Transistor BC548**
- **1 Resistor de 1kΩ** (protege a base do transistor)
- **1 LED**
- **1 Resistor de 330Ω** (limita a corrente do LED)
- **1 Fonte de 5V** (pode ser uma pilha ou um Arduino)

### 🔧 **Como Montar:**
1. **Base (B)** conecta-se ao **GPIO de um microcontrolador** ou um botão com um **resistor de 1kΩ**.
2. **Coletor (C)** conecta-se ao **positivo do LED** (com resistor de 330Ω).
3. **Emissor (E)** vai para o **GND**.

### 🔄 **Funcionamento:**
- Quando o **GPIO** envia um sinal (3.3V ou 5V), uma pequena corrente entra na **Base**.
- O transistor **liga** e permite uma corrente maior fluir do **Coletor para o Emissor**.
- O **LED acende!**
- Quando o GPIO desativa o sinal (0V), a corrente para e o LED **apaga**.

---

## 📌 **Resumo Final**
✅ O transistor **controla** o fluxo de corrente.  
✅ Funciona como uma **chave eletrônica** ou **amplificador**.  
✅ Pequenas correntes na **Base** podem ativar **grandes correntes no Coletor**.  
✅ É essencial para **sensores, motores, amplificadores, LEDs e circuitos digitais**.

🔎 **Conclusão:** O transistor é um **super-herói** da eletrônica! 🦸‍♂️⚡ Ele pode **ligar/desligar circuitos**, **ampliar sinais** e está presente em **todos os dispositivos eletrônicos modernos**! 🚀


Vamos nos concentrar nos itens em negrito.

Quando se injeta uma pequena corrente positiva no pino B, uma avalanche de corrente é conduzida do pino C para o E.


<img src="https://github.com/agodoi/m05-semana06/blob/main/imgs/transistor.jpeg" width="600">


O que vamos usar são esses possíveis modelos:


<img src="https://github.com/agodoi/m05-semana06/blob/main/imgs/transistor-bc548.jpg" width="300">
<img src="https://github.com/agodoi/m05-semana06/blob/main/imgs/transistor-tip41.png" width="300">
