- [back](https://github.com/0joseDark/my-programming-language/blob/main/doc-en/README.md)
### 📄 Example of Initial Structure for `Hibrido-AI-bot.md`

# 🤖 Hybrid AI Bot/Robot

A hybrid project that combines artificial intelligence and robotics to create an intelligent robot capable of communicating with humans, executing physical commands, and learning from the environment.

## 🎯 Objectives

- Integrate AI (chatbot) with a physical robot (Arduino/Raspberry Pi)
- Allow control via text and voice commands
- Learn simple patterns using machine learning
- Develop a graphical interface for control and feedback

## 🧠 Artificial Intelligence

- Language: Python  
- Libraries: `transformers`, `speech_recognition`, `pyttsx3`  
- Features:
  - Response to text commands
  - Response to voice commands
  - Text generation
  - Intent recognition

## 🔧 Robotics

- Platform: Arduino Mega / Raspberry Pi  
- Communication: USB / Serial / Bluetooth / Wi-Fi  
- Components:
  - Servos, DC motors
  - Distance sensors
  - Status LEDs  
- Functions:
  - Movement (forward, backward, left, right)
  - Obstacle reactions
  - Execution of AI commands

## 💻 Interface

- Graphical interface in Python (Tkinter or PyQt)
- Buttons for manual commands
- Text boxes for dialog with the bot
- Robot status feedback

## 📡 Communication

- Serial (Python ↔ Arduino)
- WebSocket (for web interface)
- Local API for commands and sensor reading

## 📂 Project Structure

```
Hibrido-AI-bot/
│
├── bot/
│   └── ai_module.py        # AI and language processing
│
├── robot/
│   └── arduino_code.ino    # Code for the Arduino
│   └── control.py          # Communication with Arduino
│
├── interface/
│   └── gui.py              # Window for interaction with the bot
│
├── docs/
│   └── Hibrido-AI-bot.md   # Project documentation
│
└── main.py                 # Entry point
```

## 🚀 How to Run

1. Install dependencies with `pip install -r requirements.txt`
2. Connect the Arduino to the PC
3. Run `python main.py`
4. Use the interface to interact with the robot

## ✅ Current Status

- [x] Functional AI module
- [x] Basic motor control
- [ ] Full integration with sensors
- [ ] Finalized graphical interface

## 📌 Next Steps

- Improve command recognition
- Train AI with custom phrases
- Optimize real-time response

## 📜 License

Open-source project under the MIT license.
