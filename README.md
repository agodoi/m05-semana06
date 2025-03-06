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

<img src="https://github.com/agodoi/m05-semana06/blob/main/imgs/transistor.jpeg" width="600">

O que vamos usar são esses possíveis modelos:

<img src="https://github.com/agodoi/m05-semana06/blob/main/imgs/transistor-bc548.jpg" width="300">

<img src="https://github.com/agodoi/m05-semana06/blob/main/imgs/transistor-tip41.png" width="300">



### (2.2) **Estrutura Básica

Um transistor bipolar (como o **BC548** e o **TIP41C**) possui **três terminais**:

- I)   **Base (B):** Controla o fluxo de corrente entre C e E.
- II)  **Coletor (C):** Entrada principal de corrente.
- III) **Emissor (E):** Saída da corrente.

👉 Existem dois tipos principais de transistores bipolares:
- **NPN** (mais comum).
- **PNP**

O **NPN** é o que usaremos como exemplo.

- N ➝ Negativo, pino Coletor (C)
- P ➝ Positivo, pino Base (B)
- N ➝ Negativo, pino Emissor (E)

## 📌 Como o Transistor Funciona?

O transistor funciona como uma **chave eletrônica** ou **amplificador de corrente**.

---

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
- ( I_C ) = corrente no **Coletor**
- ( I_B ) = corrente na **Base**
- ( β ) (ou "ganho") = fator de amplificação do transistor. Todo modelo de transistor tem um β exclusivo. O β indica o quanto sensível ele é para liberar o fluxo de corrente entre C e E a partir de uma excitação de B. Valores típicos: 100 < β < 600. Precisa entrar no datasheet para saber o valore exato do seu transistor.

**Exemplo prático:**  
- Um microfone capta um som muito fraco (corrente pequena).
- O transistor amplifica essa corrente e a envia para um alto-falante.
- O som sai alto e audível!

## Resumo:

**(a)** Transistor possui 3 pinos: Coletor (C), Base (B) e Emissor (E). 
**(b)** Existe 2 tipos de transistor: **NPN** e PNP.
**(c)** Todo transistor possui dois modos de trabalho: **Chave Liga-desliga** e Amplificador

---

## Prática (1)

Vamos acender um **LED** controlado por um **transistor NPN (BC548)**.

### 🛠️ Componentes:
- **1 Transistor BC548**
- **1 Resistor de 1MΩ** (usar de divisor de tensão com o seu corpo)
- **1 LED**
- **1 Resistor de 330Ω** (limita a corrente do LED)
- **1 Fonte de 5V** (pode ser uma pilha ou um Arduino)

### 🔧 Como Montar: siga exatamente o circuito da imagem

<img src="https://github.com/agodoi/m05-semana06/blob/main/imgs/arduino-led-bc548.png" width="1000">


### 🔄 Funcionamento:
- Quando você tocar no nó que une pino (B) e R de 1MΩ e o **fio laranja**, o seu corpo liberará uma pequena corrente na entrada da base.
- O transistor **liga** e permite uma corrente maior fluir do **Coletor para o Emissor**.
- O **LED acende!**
- Quando você remove o seu dedo, desativa o sinal (0V), a corrente para e o LED **apaga**.

## 📌 **Resumo Final**
✅ O transistor **controla** o fluxo de corrente.  
✅ Funciona como uma **chave eletrônica** ou **amplificador**.  
✅ Pequenas correntes na **Base** podem ativar **grandes correntes no Coletor**.  
✅ É essencial para **sensores, motores, amplificadores, LEDs e circuitos digitais**.

🔎 **Conclusão:** O transistor é um **super-herói** da eletrônica! 🦸‍♂️⚡ Ele pode **ligar/desligar circuitos**, **ampliar sinais** e está presente em **todos os dispositivos eletrônicos modernos**! 🚀
 



### 🏫 Aula Prática: **Demonstrando o Funcionamento do Transistor BC548 com Arduino e Monitor Plotter** 📊✨

#### 🎯 **Objetivo:**
Nesta aula, vamos utilizar um **transistor BC548** como um **amplificador de corrente**, controlado pelo **Arduino Uno**. Através do **Monitor Plotter** do Arduino IDE, analisaremos a variação de tensão na **Base** e no **Coletor**, visualizando como o transistor se comporta ao ligar e desligar um LED.

---

## 🛠️ **Materiais Necessários:**
- 1 **Arduino Uno**
- 1 **Transistor NPN BC548**
- 1 **Resistor de 1kΩ** (para a base do transistor)
- 1 **Resistor de 330Ω** (para limitar corrente do LED)
- 1 **LED**
- 1 **Potenciômetro de 10kΩ** (para controlar a corrente na Base)
- **Fios jumper**
- **Protoboard**

---

## 🔌 **Esquema de Ligação (Circuito)**

```plaintext
              +5V Arduino
                 │
         +───────┴───+
         │  Potenciômetro  │
         +───┬────┬───+
             │    │
             │    └───> Pino A0 (Arduino)  ← (Lê a tensão da Base)
             │
             ├──> Resistor 1kΩ
             │
             │
            Base do BC548
             │
        Coletor ───> Resistor 330Ω ───> LED ───> GND
             │
        Emissor ───> GND
```

---

## 🎛️ **Como Funciona?**
1. **O Potenciômetro** ajusta a corrente que entra na **Base do transistor**.
2. O **Arduino lê a tensão da Base** (pino A0).
3. O transistor controla a corrente no **Coletor → Emissor**, acendendo ou apagando o LED.
4. O **Monitor Plotter** exibe a relação entre a tensão na **Base** e no **Coletor**.
5. Conforme giramos o **potenciômetro**, podemos visualizar a **zona de corte**, **saturação** e o **modo linear** do transistor.

---

## 💻 **Código para o Arduino**

```cpp
#define BASE_PIN A0  // Pino do potenciômetro (Base do transistor)
#define COLETOR_PIN A1 // Pino conectado ao Coletor
#define LED_PIN 9  // Pino PWM para o LED (pode simular a corrente no coletor)

void setup() {
    Serial.begin(9600);
    pinMode(LED_PIN, OUTPUT);
}

void loop() {
    int baseVoltage = analogRead(BASE_PIN);  // Lê a tensão na Base
    int coletorVoltage = analogRead(COLETOR_PIN);  // Lê a tensão no Coletor

    // Converte para volts (Arduino opera de 0 a 5V com resolução de 1024 bits)
    float vBase = baseVoltage * (5.0 / 1023.0);
    float vColetor = coletorVoltage * (5.0 / 1023.0);

    // Controla o brilho do LED com a leitura da Base (simulando corrente no Coletor)
    analogWrite(LED_PIN, map(baseVoltage, 0, 1023, 0, 255));

    // Envia valores para o Monitor Plotter do Arduino
    Serial.print("Base: ");
    Serial.print(vBase);
    Serial.print("V  ");

    Serial.print("Coletor: ");
    Serial.print(vColetor);
    Serial.println("V");

    delay(100);
}
```

---

## 📊 **O que esperar no Monitor Plotter?**
- Quando giramos o **potenciômetro**, vemos a tensão na **Base** aumentando ou diminuindo.
- A tensão no **Coletor** muda conforme a Base é polarizada.
- No **modo de corte** (Base ≈ 0V), o LED **fica apagado**.
- No **modo de saturação** (Base > 0.7V), o LED **acende totalmente**.
- No **modo ativo** (entre 0.2V e 0.7V), o LED **varia o brilho** proporcionalmente.

---

## 📌 **Conclusão**
Nesta aula prática, conseguimos visualizar no **Monitor Plotter** do Arduino como a tensão na **Base** afeta a corrente no **Coletor** do transistor. Isso nos permitiu demonstrar o funcionamento do **transistor BC548** como um **interruptor eletrônico** ou um **amplificador de sinal**.

✅ **Demonstração clara dos estados de operação do transistor!**  
✅ **Interatividade com controle de um LED!**  
✅ **Monitor Plotter ajuda a visualizar a relação entre Base e Coletor!**  

🔎 **Exploração extra:** Experimente substituir o LED por um motor pequeno ou um relé para ver como o transistor pode controlar dispositivos mais potentes! 🚀

---

### 🔥 **O que achou dessa aula prática? Algo a mais que gostaria de adicionar?** 🚀



