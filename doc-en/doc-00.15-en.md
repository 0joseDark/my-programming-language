# ✅ **Robot & Drone Simulator with Qt Interface and Physics Calculations**

## 🔧 Components by System

### 🛸 **Drone (Quadcopter):**

* Microcontroller: Arduino or STM32
* 4 Brushless Motors + 4 ESCs
* Li-Po Battery
* MPU6050 Sensor (gyroscope and accelerometer)
* Formulas used: thrust, torque, PID

### 🤖 **Mobile Robot (wheels or legs):**

* Arduino Mega
* 2 DC motors or servos per leg
* H-Bridge (e.g., L298N)
* Ultrasonic sensor (HC-SR04) or camera
* Formulas: acceleration, torque, balance

---

## 🧠 Explained Formulas

| Formula                          | Usage                          |
| -------------------------------- | ------------------------------ |
| `F = m·a`                        | Thrust and locomotion force    |
| `τ = F·r`                        | Torque in motors               |
| `R = ρ·l/A`                      | Resistance in wires            |
| `t = R·C`                        | RC sensor charge time          |
| `V(t) = -V₀·e^(-t/RC)`           | Capacitor discharge            |
| `E = ½·m·v²`                     | Kinetic energy                 |
| `η = (Output / Input) × 100%`    | Mechanical efficiency          |
| `u(t) = Kp·e + Ki·∫e + Kd·de/dt` | PID controller (stabilization) |

---

## 🔍 Applied Examples

* **Drone**: required thrust to lift a mass
* **Robot**: torque needed to climb a ramp
* **Sensors**: RC response time and wire resistance

---

## 🖥️ Qt Interface (Python)

### Features:

* Simulations with variable input: **Force**, **Torque**, **Resistance**, **RC Time**
* **Interactive graphs** using `matplotlib`
* **Automatic logging** of calculations (last 10 visible)
* **Intuitive menu** with sub-options for each calculation
* Compatible with **Windows 10**, **Ubuntu**, and **macOS**

### Extras:

* **Saving results** to `.log` or `.csv`
* **PID simulation** with `Kp`, `Ki`, `Kd`, initial error and setpoint
* **Energy & Efficiency** options in the menu
* Modular: each calculation handled in a separate function/module

---

## 📡 Integration with Real Sensors (MPU6050)

### Arduino Mega:

* Reads accelerations (X, Y, Z) and rotations (Pitch, Roll, Yaw)
* Sends data via serial port

### Python (PyQt5):

* Serial reading using `pyserial`
* Real-time graph of accelerations (X, Y, Z)
* Plan for artificial horizon using gyroscope

---

## 📁 Modular Project Structure

| File / Module                 | Function                      |
| ----------------------------- | ----------------------------- |
| `main.py`                     | Main menu with Qt             |
| `modulos/simulador_fisico.py` | Physical calculations and GUI |
| `sensor_plot.py`              | Real-time sensor plots        |
| `pid.py`                      | PID simulator                 |
| `log.py`                      | Log management                |

---

## 📊 PID Simulator

* Implements the full PID formula
* Allows testing stability with various `Kp`, `Ki`, `Kd` values
* Graph showing response over time

---

## 🛰️ Artificial Horizon (planned)

* Convert `gx`, `gy` into pitch/roll angles
* Visualize “horizon” using `matplotlib` or `PyQtGraph`
* Simulates 3D movement of the drone or robot

---

## 📦 Installation (requirements)

```bash
pip install pyqt5 pyserial matplotlib
```

---

## ✅ Conclusion

This application provides:

| Feature                      | Available |
| ---------------------------- | --------- |
| Physics calculations         | ✅         |
| Qt graphical interface       | ✅         |
| PID simulation               | ✅         |
| Real sensor reading          | ✅         |
| Interactive charts           | ✅         |
| Automatic logging            | ✅         |
| Windows/Ubuntu/macOS support | ✅         |

