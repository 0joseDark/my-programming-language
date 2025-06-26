### ✅ Componentes principais:

#### **Drone (Quadricóptero)**:

* 1 microcontrolador (ex: Arduino ou STM32)
* 4 ESCs (controladores de velocidade electrónicos)
* 4 motores brushless
* 1 bateria Li-Po
* 1 módulo giroscópio/acelerómetro (ex: MPU6050)
* Fórmulas: empuxo, torque, PID

#### **Robô Móvel (com rodas ou pernas)**:

* 1 Arduino Mega
* 2 motores DC ou servos por perna (ou roda)
* Sensor ultrassónico (HC-SR04)
* Sensor de linha ou câmera
* Ponte H (ex: L298N)
* Fórmulas: velocidade, aceleração, torque, equilíbrio

---

### 🖼️ **Imagem do esquema completo** com circuitos e fórmulas:
---
## 🧠 FÓRMULAS E EXPLICAÇÕES

### 1. **Força: $F = ma$**

**F** = força (N),
**m** = massa (kg),
**a** = aceleração (m/s²)
➡️ **Usada para calcular o empuxo necessário** nos motores do drone ou a força de locomoção no robô.

---

### 2. **Torque (esforço rotacional): $\tau = \rho \dfrac{l}{A}$**

**$\tau$** = torque (N·m)
**$\rho$** = densidade do material ou massa volúmica
**l** = comprimento
**A** = área
➡️ Esta fórmula pode representar **resistência mecânica** ou **perda em cabos**. Em motores, torque também pode ser $\tau = F \cdot r$, com **r** sendo o raio.

---

### 3. **Tempo de carga RC: $t = RC$**

**R** = resistência (Ω),
**C** = capacidade (F)
➡️ Define o **tempo de resposta dos circuitos** RC (muito usado em filtros e sensores analógicos).

---

### 4. **Resistência em função da geometria: $R = \rho \dfrac{l}{A}$**

**ρ** = resistividade do material,
**l** = comprimento do fio,
**A** = secção do fio
➡️ Útil para calcular perdas nos cabos do drone ou robô.

---

### 5. **Descarga de condensador: $V(t) = -V_0 e^{-t/\tau}$**

**V(t)** = voltagem ao tempo t,
**$V_0$** = voltagem inicial,
**τ = RC**
➡️ Usado para prever o comportamento de sensores analógicos e temporizadores.

---

## 🧪 EXEMPLOS PRÁTICOS

---

### ✅ **Drone (quadricóptero)**

#### 🟦 Exemplo 1: Cálculo da força total necessária para levantar o drone

* Massa do drone: $m = 1.5 \text{ kg}$
* Aceleração necessária: $a = 9.81 \text{ m/s²}$ (gravidade)

**F = ma = 1.5 × 9.81 = 14.715 N**

➡️ Cada hélice deve gerar pelo menos 1/4 dessa força:
**F\_motor = 14.715 / 4 = 3.68 N**

---

#### 🟦 Exemplo 2: Tempo de carga de um sensor analógico

* $R = 10\text{kΩ}$, $C = 100\mu\text{F}$

**t = RC = 10,000 × 0.0001 = 1 \text{ segundo}**

➡️ O sensor demora 1 segundo a responder completamente.

---

### ✅ **Robô com rodas ou pernas**

#### 🟩 Exemplo 1: Torque necessário para subir uma rampa

* Força: $F = 2 \text{ N}$,
* Raio da roda: $r = 0.05 \text{ m}$

**$\tau = F \cdot r = 2 \cdot 0.05 = 0.1 \text{ N·m}$**

➡️ O motor tem de fornecer 0.1 N·m para subir.

---

#### 🟩 Exemplo 2: Resistência de um cabo de alimentação

* Resistividade do cobre $\rho = 1.68 × 10^{-8} \, \Omega·m$,
* Comprimento: $l = 2 \text{ m}$,
* Secção: $A = 1 \text{ mm}^2 = 1×10^{-6} \, m^2$

**$R = \rho \dfrac{l}{A} = 1.68×10^{-8} \cdot \dfrac{2}{1×10^{-6}} = 0.0336\, \Omega$**

➡️ A resistência total do fio é baixa, mas afeta motores de alta corrente.

---

## 📌 RESUMO

| Fórmula                                          | Utilização                            |
| ------------------------------------------------ | ------------------------------------- |
| $F = ma$                                         | Empuxo, aceleração, locomoção         |
| $\tau = F \cdot r$ ou $\tau = \rho \dfrac{l}{A}$ | Torque, perda em fios                 |
| $t = RC$                                         | Tempo de resposta de sensores         |
| $R = \rho \dfrac{l}{A}$                          | Resistência de cabos e trilhos        |
| $V(t) = -V_0 e^{-t/\tau}$                        | Decaimento de voltagem em sensores RC |

---

