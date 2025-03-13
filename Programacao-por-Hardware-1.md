### Programação por Hardware com Arduino Mega e um Portátil via USB

A **Programação por Hardware** utilizando o **Arduino Mega** e um portátil com portas **USB** envolve a criação de código que interage diretamente com os componentes eletrónicos conectados ao **Arduino**. Isto permite controlar motores, LEDs, sensores e outros dispositivos físicos através de comandos enviados pelo computador.

---

## 1. **Materiais Necessários**
- **Arduino Mega 2560**
- **Cabo USB (Tipo A para Tipo B)**
- **Computador portátil (Windows/Linux/macOS)**
- **Software Arduino IDE**
- **Drivers para Arduino Mega** (caso seja necessário)
- **Componentes eletrónicos** (sensores, LEDs, motores, etc.)

---

## 2. **Instalar e Configurar o Ambiente**
1. **Instalar o Arduino IDE**  
   - Descarregar a versão mais recente em: [https://www.arduino.cc/en/software](https://www.arduino.cc/en/software).
   - Instalar normalmente no seu sistema operativo.

2. **Ligar o Arduino Mega ao Portátil**
   - Usar o cabo **USB Tipo A para Tipo B** para conectar o **Arduino Mega** ao portátil.
   - Se necessário, instalar os **drivers** para que o computador reconheça a porta **COM** correspondente.

3. **Selecionar a Placa no Arduino IDE**
   - Abrir o **Arduino IDE**.
   - Ir a **Ferramentas → Placa → Arduino Mega 2560**.
   - Em **Ferramentas → Porta**, selecionar a porta **COM** atribuída ao Arduino.

---

## 3. **Escrever e Enviar Código para o Arduino**
Agora pode programar o **Arduino Mega** com código C++ diretamente no **Arduino IDE**.  

### Exemplo: Acender um LED no pino 13
```cpp
void setup() {
  pinMode(13, OUTPUT);  // Define o pino 13 como saída
}

void loop() {
  digitalWrite(13, HIGH); // Acende o LED
  delay(1000); // Espera 1 segundo
  digitalWrite(13, LOW); // Apaga o LED
  delay(1000); // Espera 1 segundo
}
```
- Após escrever o código, clique em **"Carregar"** (botão de seta para a direita).
- O código será compilado e enviado para o **Arduino Mega**.
- O LED embutido no pino **13** começará a piscar.

---

## 4. **Comunicação entre o Arduino Mega e o Portátil (Serial)**
O **Arduino Mega** pode comunicar com o portátil através da **porta USB**, usando a comunicação **Serial**.

### Exemplo: Enviar e Receber Dados pelo Monitor Serial
Este exemplo permite enviar mensagens do **Arduino** para o **portátil** e vice-versa.

#### Código para o Arduino:
```cpp
void setup() {
  Serial.begin(9600); // Inicia a comunicação Serial a 9600 baud
}

void loop() {
  Serial.println("Arduino Mega ligado!"); // Envia mensagem para o portátil
  delay(1000); // Aguarda 1 segundo
}
```
- Após carregar o código, abra o **Monitor Serial** no Arduino IDE (**Ferramentas → Monitor Serial**).
- Verá a mensagem "Arduino Mega ligado!" a aparecer continuamente.

Se quiser receber comandos do computador, pode modificar o código:
```cpp
void setup() {
  Serial.begin(9600);
}

void loop() {
  if (Serial.available()) { // Verifica se há dados recebidos
    char comando = Serial.read(); // Lê o comando enviado pelo portátil
    Serial.print("Recebi: ");
    Serial.println(comando); // Retorna o que recebeu
  }
}
```
Agora, se escrever algo no **Monitor Serial**, o Arduino devolverá o mesmo texto.

---

## 5. **Controlar Dispositivos Físicos pelo Portátil**
O **Arduino Mega** pode receber comandos via **USB** para controlar **motores, LEDs, servos e outros dispositivos**.

### Exemplo: Controlar um LED via USB
#### Código para o Arduino:
```cpp
void setup() {
  pinMode(13, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  if (Serial.available()) {
    char comando = Serial.read();
    if (comando == '1') {
      digitalWrite(13, HIGH); // Acende o LED
      Serial.println("LED ON");
    }
    if (comando == '0') {
      digitalWrite(13, LOW); // Apaga o LED
      Serial.println("LED OFF");
    }
  }
}
```
#### Código Python no Portátil para Controlar o LED:
```python
import serial

porta_serial = serial.Serial("COM3", 9600)  # Substituir COM3 pela porta correta
while True:
    comando = input("Digite 1 para acender ou 0 para apagar: ")
    porta_serial.write(comando.encode())  # Envia o comando para o Arduino
    print(porta_serial.readline().decode())  # Lê a resposta do Arduino
```
Agora, ao digitar **"1"**, o LED acende, e ao digitar **"0"**, o LED apaga.

---

## 6. **Ligar Motores e Sensores**
Além de LEDs, pode ligar **motores DC, motores de passo, servos, sensores de temperatura, botões, displays, etc.**.

### Exemplo: Controlar um Servo Motor via USB
#### Código para o Arduino:
```cpp
#include <Servo.h>

Servo meuServo;

void setup() {
  meuServo.attach(9); // Servo ligado ao pino 9
  Serial.begin(9600);
}

void loop() {
  if (Serial.available()) {
    int angulo = Serial.parseInt(); // Lê um número enviado pelo PC
    if (angulo >= 0 && angulo <= 180) {
      meuServo.write(angulo); // Move o servo para o ângulo desejado
      Serial.print("Servo em: ");
      Serial.println(angulo);
    }
  }
}
```
#### Código Python no Portátil para Controlar o Servo:
```python
import serial

porta_serial = serial.Serial("COM3", 9600)  # Substituir COM3 pela porta correta
while True:
    angulo = input("Digite um ângulo (0-180): ")
    porta_serial.write(angulo.encode())  # Envia o ângulo para o Arduino
    print(porta_serial.readline().decode())  # Exibe a resposta
```
Agora pode **controlar o servo motor digitando ângulos de 0 a 180 graus no terminal Python**.

---

## 7. **Conclusão**
A **Programação por Hardware** com o **Arduino Mega** e um portátil via **USB** permite:
- **Escrever código diretamente no Arduino**.
- **Comunicar com o PC via Serial** para envio e receção de dados.
- **Controlar dispositivos físicos como LEDs, motores e sensores**.
- **Criar aplicações no PC que interagem com o Arduino em tempo real**.

Isto é essencial para projetos de **automação, robótica e IoT**
