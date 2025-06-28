### ✅ **Main Components**

#### **Drone (Quadcopter):**

* 1 microcontroller (e.g., Arduino or STM32)
* 4 ESCs (electronic speed controllers)
* 4 brushless motors
* 1 Li-Po battery
* 1 gyroscope/accelerometer module (e.g., MPU6050)
* Formulas: thrust, torque, PID

#### **Mobile Robot (with wheels or legs):**

* 1 Arduino Mega
* 2 DC motors or servos per leg (or wheel)
* Ultrasonic sensor (HC-SR04)
* Line sensor or camera
* H-Bridge (e.g., L298N)
* Formulas: speed, acceleration, torque, balance

---

### 🧠 FORMULAS AND EXPLANATIONS

1. **Force: \$F = ma\$**
   Used to calculate required **thrust** for drone motors or movement force for robots.

2. **Torque: \$\tau = \rho \dfrac{l}{A}\$** or \$\tau = F \cdot r\$
   For rotational force or estimating losses in wires.

3. **RC Time: \$t = RC\$**
   Used in filters and sensor response time.

4. **Resistance: \$R = \rho \dfrac{l}{A}\$**
   Used to estimate wire losses.

5. **Capacitor Discharge: \$V(t) = -V\_0 e^{-t/\tau}\$**
   Used for analog signal behavior prediction.

---

### 🧪 PRACTICAL EXAMPLES

**Drone – Force calculation:**
If mass = 1.5 kg, acceleration = 9.81 m/s² →
**F = 1.5 × 9.81 = 14.715 N**,
Each motor ≈ 3.68 N.

**Robot – Torque to climb a ramp:**
If F = 2 N and r = 0.05 m →
**τ = 0.1 N·m**

**Sensor RC time (e.g., analog input):**
R = 10kΩ, C = 100µF → t = 1 second

**Cable resistance example:**
ρ = 1.68×10⁻⁸, l = 2 m, A = 1 mm² →
**R = 0.0336 Ω**

---

### ✅ GUI INTERFACE (with PyQt5)

* Menu: “Simulation”

  * Options: “Force”, “Torque”, “Resistance”, “RC Time”
* Buttons: “Calculate”, “Exit”
* Input fields for variables
* Result shown in window

---

### ✅ PROGRAM FEATURES

* Interactive GUI for each formula
* Shows result and formula
* Graph with `matplotlib`
* Saves logs (`.log` or `.csv`)
* Reads last 10 calculations
* Real-time sensor reader (Arduino MPU6050)
* PID simulator
* Modular Qt application with menu

---

### 📁 APPLICATION STRUCTURE

* `main.py` – Main menu
* `modulos/` – Simulations (force, torque...)
* `pid.py` – PID controller
* `sensor_plot.py` – Real-time MPU6050 reader with plot
* `log.py` – Logging and reading functions

---

### ✅ SYSTEM COMPATIBILITY

* ✅ Windows 10
* ✅ Ubuntu (via `apt install python3-pyqt5`)
* ✅ macOS (via `pip3 install PyQt5`)
* ✅ Raspberry Pi with Arduino (via USB/serial)
