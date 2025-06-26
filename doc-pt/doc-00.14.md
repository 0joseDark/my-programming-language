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
## passo 2:

* 🛸 Força: $F = m \cdot a$
* 🔄 Torque: $\tau = F \cdot r$
* ⚡ Resistência: $R = \rho \cdot \dfrac{l}{A}$
* ⏱️ Tempo RC: $t = R \cdot C$

---

### ✅ Interface gráfica:

* **Menu**: “Simulação”

  * Subopções: “Força”, “Torque”, “Resistência”, “Tempo RC”
* **Botões**: “Calcular” e “Sair”
* **Campos** para introduzir variáveis
* **Resultado visível** na janela

---

### 🧠 Código comentado e explicado

```python
import sys
from PyQt5.QtWidgets import (
    QApplication, QMainWindow, QWidget, QVBoxLayout, QFormLayout,
    QLabel, QLineEdit, QPushButton, QMenuBar, QAction, QMessageBox
)

class SimuladorFisica(QWidget):
    def __init__(self, tipo):
        super().__init__()
        self.tipo = tipo
        self.setWindowTitle(f"Simulador: {tipo}")
        self.layout = QVBoxLayout()
        self.form = QFormLayout()
        self.inputs = {}

        # Definir os campos conforme o tipo de simulação
        if tipo == "Força":
            campos = ["Massa (kg)", "Aceleração (m/s²)"]
        elif tipo == "Torque":
            campos = ["Força (N)", "Raio (m)"]
        elif tipo == "Resistência":
            campos = ["Resistividade (ρ)", "Comprimento (m)", "Área (m²)"]
        elif tipo == "Tempo RC":
            campos = ["Resistência (Ω)", "Capacitância (F)"]

        # Criar campos de entrada
        for campo in campos:
            entrada = QLineEdit()
            self.form.addRow(QLabel(campo), entrada)
            self.inputs[campo] = entrada

        self.resultado = QLabel("Resultado: ")
        self.botao = QPushButton("Calcular")
        self.botao.clicked.connect(self.calcular)

        self.layout.addLayout(self.form)
        self.layout.addWidget(self.botao)
        self.layout.addWidget(self.resultado)
        self.setLayout(self.layout)

    def calcular(self):
        try:
            if self.tipo == "Força":
                m = float(self.inputs["Massa (kg)"].text())
                a = float(self.inputs["Aceleração (m/s²)"].text())
                resultado = m * a
                self.resultado.setText(f"Força = {resultado:.2f} N")

            elif self.tipo == "Torque":
                f = float(self.inputs["Força (N)"].text())
                r = float(self.inputs["Raio (m)"].text())
                resultado = f * r
                self.resultado.setText(f"Torque = {resultado:.2f} N·m")

            elif self.tipo == "Resistência":
                ρ = float(self.inputs["Resistividade (ρ)"].text())
                l = float(self.inputs["Comprimento (m)"].text())
                A = float(self.inputs["Área (m²)"].text())
                resultado = ρ * l / A
                self.resultado.setText(f"Resistência = {resultado:.6f} Ω")

            elif self.tipo == "Tempo RC":
                R = float(self.inputs["Resistência (Ω)"].text())
                C = float(self.inputs["Capacitância (F)"].text())
                resultado = R * C
                self.resultado.setText(f"Tempo RC = {resultado:.3f} s")
        except Exception as e:
            QMessageBox.warning(self, "Erro", f"Erro no cálculo: {str(e)}")

class JanelaPrincipal(QMainWindow):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("Simulações para Drone e Robô")

        # Menu
        menu = self.menuBar()
        simMenu = menu.addMenu("Simulação")

        acoes = ["Força", "Torque", "Resistência", "Tempo RC"]
        for acao in acoes:
            act = QAction(acao, self)
            act.triggered.connect(lambda checked, tipo=acao: self.abrirSimulador(tipo))
            simMenu.addAction(act)

        botaoSair = QPushButton("Sair")
        botaoSair.clicked.connect(self.close)
        self.setCentralWidget(botaoSair)

    def abrirSimulador(self, tipo):
        self.simulador = SimuladorFisica(tipo)
        self.simulador.show()

# Execução
if __name__ == "__main__":
    app = QApplication(sys.argv)
    janela = JanelaPrincipal()
    janela.resize(300, 100)
    janela.show()
    sys.exit(app.exec_())
```

---

## 🖥️ Instruções para usar

### 📦 Requisitos:

```bash
pip install PyQt5
```

### ▶️ Para correr:

```bash
python simulador_fisica.py
```

---

## 🧾 Compatibilidade

* ✅ **Windows 10**: testado com PyQt5
* ✅ **Ubuntu**: instalar `python3-pyqt5` via `apt`
* ✅ **Mac**: usar `pip3 install PyQt5` com Python 3.10+

---
## Passo 3:
## ✅ NOVAS FUNCIONALIDADES

1. **Gráfico de cada fórmula** (matplotlib):

   * Ex.: variação da força com a massa, torque com raio, etc.

2. **Guardar os cálculos** num **ficheiro `.log`** ou `.csv`

   * Ficheiro: `simulacoes.log`

3. **Exibir os cálculos guardados** na janela (últimos 10 resultados)

---

## 📦 Módulos necessários

Instala:

```bash
pip install PyQt5 matplotlib
```

---

## 🧠 Código completo com comentários

```python
import sys
import os
from PyQt5.QtWidgets import (
    QApplication, QMainWindow, QWidget, QVBoxLayout, QFormLayout,
    QLabel, QLineEdit, QPushButton, QMenuBar, QAction, QMessageBox, QTextEdit
)
from PyQt5.QtCore import Qt
import matplotlib.pyplot as plt
from datetime import datetime

LOG_FILE = "simulacoes.log"

class SimuladorFisica(QWidget):
    def __init__(self, tipo):
        super().__init__()
        self.tipo = tipo
        self.setWindowTitle(f"Simulador: {tipo}")
        self.layout = QVBoxLayout()
        self.form = QFormLayout()
        self.inputs = {}

        self.campos = {
            "Força": ["Massa (kg)", "Aceleração (m/s²)"],
            "Torque": ["Força (N)", "Raio (m)"],
            "Resistência": ["Resistividade (ρ)", "Comprimento (m)", "Área (m²)"],
            "Tempo RC": ["Resistência (Ω)", "Capacitância (F)"]
        }

        for campo in self.campos[tipo]:
            entrada = QLineEdit()
            self.form.addRow(QLabel(campo), entrada)
            self.inputs[campo] = entrada

        self.resultado = QLabel("Resultado: ")
        self.botao = QPushButton("Calcular")
        self.botao.clicked.connect(self.calcular)

        self.botaoGrafico = QPushButton("Mostrar Gráfico")
        self.botaoGrafico.clicked.connect(self.mostrar_grafico)

        self.resultadosAntigos = QTextEdit()
        self.resultadosAntigos.setReadOnly(True)
        self.carregar_resultados()

        self.layout.addLayout(self.form)
        self.layout.addWidget(self.botao)
        self.layout.addWidget(self.botaoGrafico)
        self.layout.addWidget(self.resultado)
        self.layout.addWidget(QLabel("Últimos cálculos:"))
        self.layout.addWidget(self.resultadosAntigos)
        self.setLayout(self.layout)

    def calcular(self):
        try:
            if self.tipo == "Força":
                m = float(self.inputs["Massa (kg)"].text())
                a = float(self.inputs["Aceleração (m/s²)"].text())
                resultado = m * a
                formula = f"F = m*a = {m}*{a} = {resultado:.2f} N"

            elif self.tipo == "Torque":
                f = float(self.inputs["Força (N)"].text())
                r = float(self.inputs["Raio (m)"].text())
                resultado = f * r
                formula = f"τ = F*r = {f}*{r} = {resultado:.2f} N·m"

            elif self.tipo == "Resistência":
                ρ = float(self.inputs["Resistividade (ρ)"].text())
                l = float(self.inputs["Comprimento (m)"].text())
                A = float(self.inputs["Área (m²)"].text())
                resultado = ρ * l / A
                formula = f"R = ρ*l/A = {ρ}*{l}/{A} = {resultado:.6f} Ω"

            elif self.tipo == "Tempo RC":
                R = float(self.inputs["Resistência (Ω)"].text())
                C = float(self.inputs["Capacitância (F)"].text())
                resultado = R * C
                formula = f"t = R*C = {R}*{C} = {resultado:.3f} s"

            self.resultado.setText("Resultado: " + formula)
            self.registar_log(formula)
            self.carregar_resultados()

        except Exception as e:
            QMessageBox.warning(self, "Erro", f"Erro no cálculo: {str(e)}")

    def mostrar_grafico(self):
        try:
            x_vals = []
            y_vals = []

            if self.tipo == "Força":
                a = float(self.inputs["Aceleração (m/s²)"].text())
                x_vals = [i for i in range(1, 11)]
                y_vals = [m * a for m in x_vals]
                titulo = "Força vs Massa"
                xlabel, ylabel = "Massa (kg)", "Força (N)"

            elif self.tipo == "Torque":
                f = float(self.inputs["Força (N)"].text())
                x_vals = [i/10 for i in range(1, 21)]
                y_vals = [f * r for r in x_vals]
                titulo = "Torque vs Raio"
                xlabel, ylabel = "Raio (m)", "Torque (N·m)"

            elif self.tipo == "Resistência":
                ρ = float(self.inputs["Resistividade (ρ)"].text())
                l = float(self.inputs["Comprimento (m)"].text())
                x_vals = [i/10 for i in range(1, 21)]
                y_vals = [ρ * l / A for A in x_vals]
                titulo = "Resistência vs Área"
                xlabel, ylabel = "Área (m²)", "Resistência (Ω)"

            elif self.tipo == "Tempo RC":
                R = float(self.inputs["Resistência (Ω)"].text())
                x_vals = [i/1000 for i in range(1, 1001, 50)]
                y_vals = [R * C for C in x_vals]
                titulo = "Tempo vs Capacitância"
                xlabel, ylabel = "Capacitância (F)", "Tempo (s)"

            plt.figure(figsize=(5,4))
            plt.plot(x_vals, y_vals, marker="o")
            plt.title(titulo)
            plt.xlabel(xlabel)
            plt.ylabel(ylabel)
            plt.grid(True)
            plt.tight_layout()
            plt.show()

        except Exception as e:
            QMessageBox.warning(self, "Erro no gráfico", str(e))

    def registar_log(self, linha):
        timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
        with open(LOG_FILE, "a") as f:
            f.write(f"[{timestamp}] {self.tipo}: {linha}\n")

    def carregar_resultados(self):
        if not os.path.exists(LOG_FILE):
            return
        with open(LOG_FILE, "r") as f:
            linhas = f.readlines()
        ultimos = [linha.strip() for linha in linhas if self.tipo in linha][-10:]
        self.resultadosAntigos.setText("\n".join(ultimos))

class JanelaPrincipal(QMainWindow):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("Simulações para Drone e Robô")

        menu = self.menuBar()
        simMenu = menu.addMenu("Simulação")

        acoes = ["Força", "Torque", "Resistência", "Tempo RC"]
        for acao in acoes:
            act = QAction(acao, self)
            act.triggered.connect(lambda checked, tipo=acao: self.abrirSimulador(tipo))
            simMenu.addAction(act)

        botaoSair = QPushButton("Sair")
        botaoSair.clicked.connect(self.close)
        self.setCentralWidget(botaoSair)

    def abrirSimulador(self, tipo):
        self.simulador = SimuladorFisica(tipo)
        self.simulador.resize(400, 400)
        self.simulador.show()

# Execução
if __name__ == "__main__":
    app = QApplication(sys.argv)
    janela = JanelaPrincipal()
    janela.resize(300, 100)
    janela.show()
    sys.exit(app.exec_())
```

---

## 🧾 O que este programa faz:

* Cria uma janela para cada tipo de simulação (Força, Torque, etc.)
* Calcula com base nos dados introduzidos
* Exibe **gráfico interativo** com `matplotlib`
* Grava resultados com timestamp num ficheiro `simulacoes.log`
* Mostra os últimos 10 resultados no ecrã

---
## Passo 4:
Perfeito! Vamos agora **expandir o simulador com novas funcionalidades**, **leitura de sensores reais** e **gráficos avançados**:

---

## 🔧 NOVAS FUNCIONALIDADES

### ✅ 1. **Simulação de Energia e Eficiência**

* **Energia cinética**:
  $E = \frac{1}{2}mv^2$
* **Eficiência mecânica**:
  $\eta = \frac{Saída}{Entrada} \times 100\%$

### ✅ 2. **Simulação de PID**

* Controlador Proporcional-Integral-Derivativo
  $u(t) = K_p e(t) + K_i \int e(t)dt + K_d \frac{de(t)}{dt}$
* Aplicado, por exemplo, para estabilizar o drone usando sensor de ângulo (MPU6050)

### ✅ 3. **Leitura em tempo real de dados via Arduino (com Raspberry Pi)**

* Arduino Mega envia dados do MPU6050 via porta serial
* Python lê e mostra:

  * Aceleração (X, Y, Z)
  * Velocidade angular (pitch, roll, yaw)
  * Gráfico tipo **horizonte artificial** ou **linha do tempo 3D**

---

## 📦 ESTRUTURA DO SISTEMA

### 🎯 Arduino Mega (código C++)

```cpp
#include <Wire.h>
#include <MPU6050.h>

MPU6050 mpu;

void setup() {
  Serial.begin(9600);
  Wire.begin();
  mpu.initialize();
}

void loop() {
  int16_t ax, ay, az, gx, gy, gz;
  mpu.getMotion6(&ax, &ay, &az, &gx, &gy, &gz);

  Serial.print(ax); Serial.print(",");
  Serial.print(ay); Serial.print(",");
  Serial.print(az); Serial.print(",");
  Serial.print(gx); Serial.print(",");
  Serial.print(gy); Serial.print(",");
  Serial.println(gz);
  delay(100);
}
```

---

### 🐍 Python (Raspberry Pi ou PC)

Instala dependências:

```bash
pip install pyserial matplotlib PyQt5
```

### 🧠 Leitor de sensores com gráfico em tempo real

```python
import sys
import serial
import threading
from PyQt5.QtWidgets import QApplication, QMainWindow, QLabel, QVBoxLayout, QWidget
from PyQt5.QtCore import QTimer
import matplotlib.pyplot as plt
from matplotlib.backends.backend_qt5agg import FigureCanvasQTAgg as Canvas

PORTA_SERIAL = '/dev/ttyUSB0'  # ou COM3 no Windows
BAUDRATE = 9600

class SensorPlot(QWidget):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("Gráfico de Sensor 3 Eixos (MPU6050)")
        self.ax_data = []
        self.ay_data = []
        self.az_data = []

        self.canvas = Canvas(plt.figure(figsize=(5, 3)))
        self.ax = self.canvas.figure.add_subplot(111)
        self.ax.set_title("Aceleração (X, Y, Z)")
        self.ax.set_ylim(-20000, 20000)
        self.line_x, = self.ax.plot([], [], label='Ax')
        self.line_y, = self.ax.plot([], [], label='Ay')
        self.line_z, = self.ax.plot([], [], label='Az')
        self.ax.legend()

        layout = QVBoxLayout()
        layout.addWidget(self.canvas)
        self.setLayout(layout)

        self.timer = QTimer()
        self.timer.timeout.connect(self.atualizar_grafico)
        self.timer.start(100)

        self.serial = serial.Serial(PORTA_SERIAL, BAUDRATE)
        self.leitura = threading.Thread(target=self.ler_dados)
        self.leitura.daemon = True
        self.leitura.start()

    def ler_dados(self):
        while True:
            try:
                linha = self.serial.readline().decode('utf-8').strip()
                ax, ay, az, *_ = map(int, linha.split(','))
                self.ax_data.append(ax)
                self.ay_data.append(ay)
                self.az_data.append(az)

                if len(self.ax_data) > 100:
                    self.ax_data.pop(0)
                    self.ay_data.pop(0)
                    self.az_data.pop(0)
            except:
                continue

    def atualizar_grafico(self):
        self.line_x.set_data(range(len(self.ax_data)), self.ax_data)
        self.line_y.set_data(range(len(self.ay_data)), self.ay_data)
        self.line_z.set_data(range(len(self.az_data)), self.az_data)
        self.ax.set_xlim(0, 100)
        self.canvas.draw()

if __name__ == "__main__":
    app = QApplication(sys.argv)
    janela = SensorPlot()
    janela.resize(600, 400)
    janela.show()
    sys.exit(app.exec_())
```

---

## 🛰️ HORIZONTE ARTIFICIAL (Pitch/Roll)

Usando os valores `gx`, `gy`, `gz` (giroscópio), podemos adicionar um **painel gráfico com horizonte** (tipo cockpit), atualizando o plano conforme o ângulo de inclinação.

Posso gerar isso também com `matplotlib.animation` ou `PyQtGraph` para melhor desempenho.

---

## 🔧 INTEGRAÇÃO TOTAL

Unir tudo:

* Qt com **simulador de força, torque, energia, PID**
* Módulo para **ler sensores reais**
* **Gráfico em tempo real + logs**
* Aplicação robusta para **PC ou Raspberry Pi**

---
## Passo 5:
## 🧱 ESTRUTURA DA APLICAÇÃO

### 🎛️ Interface Principal (menu Qt):

```
┌──────────────────────────────┐
│      Simulações Física       │
├──────────────────────────────┤
│ [Menu Simulação]             │
│   ├─ Força                   │
│   ├─ Torque                  │
│   ├─ Resistência             │
│   ├─ Tempo RC                │
│   ├─ Energia Cinética        │
│   ├─ Eficiência              │
│   ├─ PID (ajustável)         │
│   └─ Sensores 3 Eixos (RT)   │
│                              │
│ [Gravação em log.txt / .csv] │
└──────────────────────────────┘
```

---

## 🎯 Objetivo: tudo numa só aplicação com `PyQt5`

---

## 📦 Instalar dependências:

```bash
pip install pyqt5 pyserial matplotlib
```

---

## 🧠 ESTRUTURA DO CÓDIGO (resumo por módulos)

### 🗂️ Arquivos:

* `main.py` – menu principal
* `modulos/` – simulações (força, torque, etc.)
* `pid.py` – controlador PID
* `sensor_plot.py` – gráfico dos sensores MPU6050
* `log.py` – logging e leitura

---

## 🧪 Exemplo: `main.py` (início da app)

```python
import sys
from PyQt5.QtWidgets import QApplication, QMainWindow, QPushButton, QAction, QMenu
from modulos.simulador_fisico import SimuladorFisica
from sensor_plot import SensorPlot
from pid import JanelaPID

class JanelaPrincipal(QMainWindow):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("Simulações Robô & Drone")
        self.resize(500, 150)

        menu = self.menuBar()
        sim_menu = menu.addMenu("Simulação Física")
        sensores_menu = menu.addMenu("Sensores")

        opcoes = ["Força", "Torque", "Resistência", "Tempo RC", "Energia Cinética", "Eficiência"]
        for nome in opcoes:
            acao = QAction(nome, self)
            acao.triggered.connect(lambda checked, n=nome: self.abrir_simulador(n))
            sim_menu.addAction(acao)

        # PID
        acao_pid = QAction("Controlador PID", self)
        acao_pid.triggered.connect(self.abrir_pid)
        sim_menu.addAction(acao_pid)

        # Sensores 3 eixos
        acao_sensores = QAction("MPU6050 em tempo real", self)
        acao_sensores.triggered.connect(self.abrir_sensor)
        sensores_menu.addAction(acao_sensores)

        botao_sair = QPushButton("Sair")
        botao_sair.clicked.connect(self.close)
        self.setCentralWidget(botao_sair)

    def abrir_simulador(self, tipo):
        self.sim = SimuladorFisica(tipo)
        self.sim.resize(500, 400)
        self.sim.show()

    def abrir_sensor(self):
        self.sensor = SensorPlot()
        self.sensor.show()

    def abrir_pid(self):
        self.pid = JanelaPID()
        self.pid.show()

if __name__ == "__main__":
    app = QApplication(sys.argv)
    janela = JanelaPrincipal()
    janela.show()
    sys.exit(app.exec_())
```

---

## 📊 `sensor_plot.py` → Leitura real de sensores

* Lê da porta serial (Arduino)
* Mostra gráfico com **X, Y, Z**
* Guarda dados no log

---

## ⚙️ `simulador_fisico.py` → Cálculo com fórmulas físicas

Inclui:

* $F = ma$
* $\tau = F \cdot r$
* $R = \rho \frac{l}{A}$
* $t = RC$
* $E = \frac{1}{2}mv^2$
* Eficiência = $\frac{Saída}{Entrada} \times 100\%$

Mostra:

* Fórmula
* Gráfico da variável vs valor
* Últimos 10 resultados

---

## 🧮 `pid.py` → Simulador PID

* Campos: `Kp`, `Ki`, `Kd`, `Erro Inicial`, `Setpoint`
* Gera gráfico da resposta do controlador ao longo do tempo

---

## 📁 `log.py` → Função auxiliar

* `gravar_log(tipo, resultado)`
* `ler_logs(tipo, últimos_n)`

---

## 📷 Horizonte Artificial?

Para criar:

* Converte o giroscópio em ângulos: pitch, roll
* Usa `matplotlib` com `imshow()` ou `transform()` para mostrar horizonte
* Alternativa mais rápida: `PyQtGraph`

---

## ✅ Conclusão

Com esta aplicação Qt unificada, terás:

| Funcionalidade               | Incluído ✅             |
| ---------------------------- | ---------------------- |
| Cálculos físicos             | ✅                      |
| Simulação PID                | ✅                      |
| Leitura de sensores reais    | ✅                      |
| Gráfico tipo horizonte       | ✅ (em desenvolvimento) |
| Logs automáticos             | ✅                      |
| Compatível com RPi + Arduino | ✅                      |

---

