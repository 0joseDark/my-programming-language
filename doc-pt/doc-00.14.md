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

