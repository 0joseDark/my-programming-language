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
