## opensim:

**OpenSimulator (or OpenSim)** is an **open-source platform** for creating **3D virtual worlds**, very similar to Second Life but with more freedom and control for the user. With OpenSim, you can build your own "metaverse" — either locally, on a private network, or publicly on the internet.

---

### 🧠 What is **OpenSimulator**?

**OpenSimulator** ([https://opensimulator.org](https://opensimulator.org)) is a **3D virtual world server** built in C# that runs on the .NET/Mono platform. It allows:

* Creating **interactive 3D environments**
* Creating **avatars**, objects, scripts, terrains, and constructions
* Multiple users interacting in the same world
* Support for **physics engines**, **voice**, **virtual currencies**, and more

---

### 🧰 Main Requirements:

| Operating System | Windows, Linux, macOS (with Mono)                            |
| ---------------- | ------------------------------------------------------------ |
| Platform         | .NET Framework or Mono                                       |
| Dependencies     | MySQL (optional), Robust.Server, 3D client (e.g., Firestorm) |

---

### 🏗️ Key Components of OpenSimulator:

| Component               | Function                                                              |
| ----------------------- | --------------------------------------------------------------------- |
| **Robust**              | Central server for authentication, inventory, avatars, remote regions |
| **OpenSim.exe**         | Main process for simulating a region (3D world)                       |
| **Region Files (.ini)** | Region configuration files                                            |
| **Grid Mode**           | Multiple regions connected to a central Robust server                 |
| **Standalone Mode**     | Everything on a single server (for local/testing use)                 |

---

### 🛠️ Basic Installation (Windows or Linux)

#### Basic steps:

1. 🔽 **Download** OpenSimulator:

   * [https://opensimulator.org/wiki/Download](https://opensimulator.org/wiki/Download)

2. 📦 **Unzip the ZIP file** into a directory

3. ⚙️ **Edit the configuration files**:

   * `OpenSim.ini` → general configuration
   * `Regions/Regions.ini` → define region name, position, and coordinates

4. 🏁 **Run the server**:

   ```bash
   mono OpenSim.exe        # On Linux/macOS with Mono
   OpenSim.exe             # On Windows
   ```

5. 📶 **Connect with a client** like **Firestorm**:

   * URL: `http://localhost:9000` (standalone mode)
   * Create an avatar account in the OpenSim terminal on first run

---

### 🧑‍💻 Basic commands in OpenSim terminal:

| Command       | Function                                 |
| ------------- | ---------------------------------------- |
| `create user` | Creates a new avatar                     |
| `show users`  | Shows online users                       |
| `load oar`    | Loads a region file (landscape, objects) |
| `save oar`    | Saves the current region state           |

---

### 🌐 Grid vs Standalone

| Mode           | Advantages                   | When to use                                 |
| -------------- | ---------------------------- | ------------------------------------------- |
| **Standalone** | Easy to configure, all local | Tests, personal worlds                      |
| **Grid**       | Scalable, separate servers   | Shared worlds, multi-user, public metaverse |

---

### 📦 Important files:

* `OpenSim.ini` – server configuration
* `Robust.HG.ini` – Robust server configuration
* `Regions/Regions.ini` – defines the world regions
* `bin/` – where OpenSim executable is located
* `oar` – "scene" files (like saved maps)

---

### 🧱 Example region (`Regions.ini`):

```ini
[MyRegion]
RegionUUID = 00000000-0000-0000-0000-000000000000
Location = 1000,1000
InternalAddress = 0.0.0.0
InternalPort = 9000
AllowAlternatePorts = False
ExternalHostName = 127.0.0.1
```

---

### 🎨 What can you create in OpenSim?

* 🏰 Build buildings, lands, seas, mountains
* 🧍‍♂️ Custom avatars
* 🎮 Interactions with scripts (Linden Scripting Language - LSL)
* 📦 Import content from Second Life
* 🛰️ Connect to public grids like OSGrid

---

### 🎓 Conclusion

**OpenSimulator** is a powerful and free platform to create your own **3D virtual world**, whether for:

* **Distance learning**
* **Training simulations**
* **Educational games**
* **Artistic experiences**
* **Private virtual communities**
