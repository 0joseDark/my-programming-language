# ✅ **Simulador Robô & Drone com Interface Qt e Cálculos Físicos**

## 🔧 Componentes por Sistema

### 🛸 **Drone (Quadricóptero)**:

* Microcontrolador: Arduino ou STM32
* 4 Motores Brushless + 4 ESCs
* Bateria Li-Po
* Sensor MPU6050 (giroscópio e acelerómetro)
* Fórmulas usadas: força (empuxo), torque, PID

### 🤖 **Robô Móvel (rodas ou pernas)**:

* Arduino Mega
* 2 motores DC ou servos por perna
* Ponte H (ex: L298N)
* Sensor ultrassónico HC-SR04 ou câmara
* Fórmulas: aceleração, torque, equilíbrio

---

## 🧠 Fórmulas Explicadas

| Fórmula                          | Utilização                      |
| -------------------------------- | ------------------------------- |
| `F = m·a`                        | Empuxo e força de locomoção     |
| `τ = F·r`                        | Torque nos motores              |
| `R = ρ·l/A`                      | Resistência em cabos            |
| `t = R·C`                        | Tempo de carga de sensores RC   |
| `V(t) = -V₀·e^(-t/RC)`           | Descarga de condensadores       |
| `E = ½·m·v²`                     | Energia cinética                |
| `η = (Saída / Entrada) × 100%`   | Eficiência mecânica             |
| `u(t) = Kp·e + Ki·∫e + Kd·de/dt` | Controlador PID (estabilização) |

---

## 🔍 Exemplos Aplicados

* **Drone**: cálculo de empuxo necessário para levantar massa.
* **Robô**: torque necessário para subir rampa.
* **Sensores**: tempo de resposta RC e resistência de fios.

---

## 🖥️ Interface Qt (Python)

### Funcionalidades:

* Simulações com entrada de variáveis: **Força**, **Torque**, **Resistência**, **Tempo RC**
* **Gráficos interativos** com `matplotlib`
* **Log automático** dos cálculos (últimos 10 visíveis)
* **Menu intuitivo** com sub-opções por tipo de cálculo
* Compatível com **Windows 10**, **Ubuntu** e **MacOS**

### Extras:

* **Gravação de resultados** em `.log` ou `.csv`
* **Simulação PID** com `Kp`, `Ki`, `Kd`, erro inicial e setpoint
* **Energia & Eficiência** adicionadas ao menu
* Modular: cada cálculo numa função/módulo separado

---

## 📡 Integração com Sensores Reais (MPU6050)

### Arduino Mega:

* Lê acelerações (X, Y, Z) e rotações (Pitch, Roll, Yaw)
* Envia via porta serial

### Python (PyQt5):

* Leitura serial com `pyserial`
* Gráfico em tempo real das acelerações (X, Y, Z)
* Planeamento para horizonte artificial (usando giroscópio)

---

## 📁 Estrutura Modular do Projeto

| Ficheiro / Módulo             | Função                               |
| ----------------------------- | ------------------------------------ |
| `main.py`                     | Menu principal com Qt                |
| `modulos/simulador_fisico.py` | Cálculos físicos e interface gráfica |
| `sensor_plot.py`              | Gráficos de sensores em tempo real   |
| `pid.py`                      | Simulador PID                        |
| `log.py`                      | Gestão de logs                       |

---

## 📊 Simulador PID

* Implementa fórmula completa do PID
* Permite testar estabilidade com diferentes valores de `Kp`, `Ki`, `Kd`
* Gráfico da resposta ao longo do tempo

---

## 🛰️ Horizonte Artificial (planeado)

* Conversão de `gx`, `gy` em ângulos (pitch/roll)
* Visualização do “horizonte” com `matplotlib` ou `PyQtGraph`
* Permite simular movimento do drone ou robô em 3D

---

## 📦 Instalação (requisitos)

```bash
pip install pyqt5 pyserial matplotlib
```
```python
# Estrutura de pastas:
# ├── main.py
# ├── modulos/
# │   ├── __init__.py
# │   ├── simulador_fisico.py
# │   └── pid.py
# ├── sensor_plot.py
# └── log.py

# =========================================
# Ficheiro: main.py
# =========================================

import sys
from PyQt5.QtWidgets import QApplication, QMainWindow, QPushButton, QAction
from modulos.simulador_fisico import SimuladorFisica
from sensor_plot import SensorPlot
from modulos.pid import JanelaPID

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

        acao_pid = QAction("Controlador PID", self)
        acao_pid.triggered.connect(self.abrir_pid)
        sim_menu.addAction(acao_pid)

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
```python
# Estrutura de pastas:
# ├── main.py
# ├── modulos/
# │   ├── __init__.py
# │   ├── simulador_fisico.py
# │   └── pid.py
# ├── sensor_plot.py
# └── log.py

# =========================================
# Ficheiro: main.py
# =========================================

import sys
from PyQt5.QtWidgets import QApplication, QMainWindow, QPushButton, QAction
from modulos.simulador_fisico import SimuladorFisica
from sensor_plot import SensorPlot
from modulos.pid import JanelaPID

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

        acao_pid = QAction("Controlador PID", self)
        acao_pid.triggered.connect(self.abrir_pid)
        sim_menu.addAction(acao_pid)

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

# =========================================
# Ficheiro: modulos/__init__.py
# =========================================

# Este ficheiro torna a pasta 'modulos' num pacote Python.

# =========================================
# Ficheiro: modulos/simulador_fisico.py
# =========================================

import os
from PyQt5.QtWidgets import QWidget, QVBoxLayout, QFormLayout, QLabel, QLineEdit, QPushButton, QTextEdit, QMessageBox
from PyQt5.QtCore import Qt
import matplotlib.pyplot as plt
from log import gravar_log, ler_logs

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
            "Tempo RC": ["Resistência (Ω)", "Capacitância (F)"],
            "Energia Cinética": ["Massa (kg)", "Velocidade (m/s)"],
            "Eficiência": ["Saída (W)", "Entrada (W)"]
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

            elif self.tipo == "Energia Cinética":
                m = float(self.inputs["Massa (kg)"].text())
                v = float(self.inputs["Velocidade (m/s)"].text())
                resultado = 0.5 * m * v**2
                formula = f"E = 0.5*m*v² = 0.5*{m}*{v}² = {resultado:.2f} J"

            elif self.tipo == "Eficiência":
                saida = float(self.inputs["Saída (W)"].text())
                entrada = float(self.inputs["Entrada (W)"].text())
                resultado = (saida / entrada) * 100
                formula = f"η = (Saída/Entrada)*100 = ({saida}/{entrada})*100 = {resultado:.2f}%"

            self.resultado.setText("Resultado: " + formula)
            gravar_log(self.tipo, formula)
            self.carregar_resultados()

        except Exception as e:
            QMessageBox.warning(self, "Erro", f"Erro no cálculo: {str(e)}")

    def mostrar_grafico(self):
        try:
            x_vals, y_vals = [], []
            titulo, xlabel, ylabel = "", "", ""

            if self.tipo == "Força":
                a = float(self.inputs["Aceleração (m/s²)"].text())
                x_vals = list(range(1, 11))
                y_vals = [m * a for m in x_vals]
                titulo = "Força vs Massa"
                xlabel, ylabel = "Massa (kg)", "Força (N)"

            elif self.tipo == "Torque":
                f = float(self.inputs["Força (N)"].text())
                x_vals = [i / 10 for i in range(1, 21)]
                y_vals = [f * r for r in x_vals]
                titulo = "Torque vs Raio"
                xlabel, ylabel = "Raio (m)", "Torque (N·m)"

            elif self.tipo == "Resistência":
                ρ = float(self.inputs["Resistividade (ρ)"].text())
                l = float(self.inputs["Comprimento (m)"].text())
                x_vals = [i / 10 for i in range(1, 21)]
                y_vals = [ρ * l / A for A in x_vals]
                titulo = "Resistência vs Área"
                xlabel, ylabel = "Área (m²)", "Resistência (Ω)"

            elif self.tipo == "Tempo RC":
                R = float(self.inputs["Resistência (Ω)"].text())
                x_vals = [i / 1000 for i in range(1, 1001, 50)]
                y_vals = [R * C for C in x_vals]
                titulo = "Tempo vs Capacitância"
                xlabel, ylabel = "Capacitância (F)", "Tempo (s)"

            plt.figure(figsize=(5, 4))
            plt.plot(x_vals, y_vals, marker="o")
            plt.title(titulo)
            plt.xlabel(xlabel)
            plt.ylabel(ylabel)
            plt.grid(True)
            plt.tight_layout()
            plt.show()

        except Exception as e:
            QMessageBox.warning(self, "Erro no gráfico", str(e))

    def carregar_resultados(self):
        ultimos = ler_logs(self.tipo, 10)
        self.resultadosAntigos.setText("\n".join(ultimos))

```
```python
# Estrutura de pastas:
# ├── main.py
# ├── modulos/
# │   ├── __init__.py
# │   ├── simulador_fisico.py
# │   └── pid.py
# ├── sensor_plot.py
# └── log.py

# =========================================
# Ficheiro: main.py
# =========================================

import sys
from PyQt5.QtWidgets import QApplication, QMainWindow, QPushButton, QAction
from modulos.simulador_fisico import SimuladorFisica
from sensor_plot import SensorPlot
from modulos.pid import JanelaPID

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

        acao_pid = QAction("Controlador PID", self)
        acao_pid.triggered.connect(self.abrir_pid)
        sim_menu.addAction(acao_pid)

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

# =========================================
# Ficheiro: modulos/__init__.py
# =========================================

# Este ficheiro torna a pasta 'modulos' num pacote Python.

# =========================================
# Ficheiro: modulos/simulador_fisico.py
# =========================================

<... conteúdo anterior do simulador_fisico.py ...>

# =========================================
# Ficheiro: modulos/pid.py
# =========================================

from PyQt5.QtWidgets import QWidget, QVBoxLayout, QLabel, QFormLayout, QLineEdit, QPushButton, QMessageBox
import matplotlib.pyplot as plt

class JanelaPID(QWidget):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("Simulador PID")
        self.layout = QVBoxLayout()
        self.form = QFormLayout()

        self.inputs = {}
        campos = ["Kp", "Ki", "Kd", "Erro Inicial", "Setpoint"]

        for campo in campos:
            entrada = QLineEdit()
            self.form.addRow(QLabel(campo), entrada)
            self.inputs[campo] = entrada

        self.botao = QPushButton("Simular")
        self.botao.clicked.connect(self.simular_pid)

        self.layout.addLayout(self.form)
        self.layout.addWidget(self.botao)
        self.setLayout(self.layout)

    def simular_pid(self):
        try:
            Kp = float(self.inputs["Kp"].text())
            Ki = float(self.inputs["Ki"].text())
            Kd = float(self.inputs["Kd"].text())
            erro_inicial = float(self.inputs["Erro Inicial"].text())
            setpoint = float(self.inputs["Setpoint"].text())

            dt = 1  # passo de tempo
            tempo_total = 50
            tempos = list(range(tempo_total))
            erros = []
            saidas = []
            integral = 0
            erro_anterior = erro_inicial
            saida = 0

            for t in tempos:
                erro = setpoint - saida
                integral += erro * dt
                derivada = (erro - erro_anterior) / dt
                saida = Kp * erro + Ki * integral + Kd * derivada
                erros.append(erro)
                saidas.append(saida)
                erro_anterior = erro

            plt.figure(figsize=(6, 4))
            plt.plot(tempos, saidas, label="Saída PID")
            plt.plot(tempos, [setpoint]*tempo_total, '--', label="Setpoint")
            plt.xlabel("Tempo")
            plt.ylabel("Saída")
            plt.title("Resposta do Controlador PID")
            plt.grid(True)
            plt.legend()
            plt.tight_layout()
            plt.show()

        except Exception as e:
            QMessageBox.warning(self, "Erro", f"Erro na simulação: {str(e)}")

```
---

## ✅ Conclusão

Esta aplicação oferece:

| Funcionalidade               | Disponível |
| ---------------------------- | ---------- |
| Cálculos físicos             | ✅          |
| Interface gráfica Qt         | ✅          |
| Simulação PID                | ✅          |
| Leitura de sensores reais    | ✅          |
| Gráficos interativos         | ✅          |
| Registo automático (log)     | ✅          |
| Suporte a Windows/Ubuntu/Mac | ✅          |

---

### ✅ 1. `modulos/simulador_fisico.py`

Contém as simulações físicas (força, torque, resistência, tempo RC, energia cinética, eficiência).
Inclui:

* Interface Qt
* Cálculo
* Gráfico com matplotlib
* Registo de logs

### ✅ 2. `modulos/pid.py`

Simulador PID com entrada de `Kp`, `Ki`, `Kd`, erro inicial e gráfico de resposta.

### ✅ 3. `sensor_plot.py`

Leitura em tempo real dos dados do sensor MPU6050 (X, Y, Z) e exibição gráfica.

### ✅ 4. `log.py`

Funções auxiliares:

* `gravar_log(tipo, resultado)`
* `ler_logs(tipo, últimos_n)`

---
### em construção
