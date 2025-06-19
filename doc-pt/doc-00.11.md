## opensim:
**OpenSimulator (ou OpenSim)** é uma plataforma **open-source** para a criação de **mundos virtuais em 3D**, muito parecida com o Second Life, mas com mais liberdade e controlo por parte do utilizador. Com o OpenSim, podes montar o teu próprio "metaverso" — seja localmente, numa rede privada ou publicamente na internet.

---

### 🧠 O que é o **OpenSimulator**?

O **OpenSimulator** ([https://opensimulator.org](https://opensimulator.org)) é um **servidor de mundos virtuais 3D** construído em C# que funciona sobre a plataforma .NET/Mono. Ele permite:

* Criar **ambientes 3D interativos**
* Criar **avatars**, objetos, scripts, terrenos e construções
* Ter múltiplos utilizadores a interagir no mesmo mundo
* Suporte a **physics engines**, **voz**, **moedas virtuais** e muito mais

---

### 🧰 Requisitos principais:

| Sistema Operativo | Windows, Linux, macOS (com Mono)                            |
| ----------------- | ----------------------------------------------------------- |
| Plataforma        | .NET Framework ou Mono                                      |
| Dependências      | MySQL (opcional), Robust.Server, cliente 3D (ex: Firestorm) |

---

### 🏗️ Componentes principais do OpenSimulator:

| Componente              | Função                                                                    |
| ----------------------- | ------------------------------------------------------------------------- |
| **Robust**              | Servidor central para autenticação, inventário, avatares, regiões remotas |
| **OpenSim.exe**         | O processo principal para simular uma região (mundo 3D)                   |
| **Region Files (.ini)** | Ficheiros de configuração de regiões                                      |
| **Grid Mode**           | Várias regiões ligadas a um Robust central                                |
| **Standalone Mode**     | Tudo num único servidor (modo local/testes)                               |

---

### 🛠️ Instalação básica (Windows ou Linux)

#### Passos básicos:

1. 🔽 **Faz o download** do OpenSimulator:

   * [https://opensimulator.org/wiki/Download](https://opensimulator.org/wiki/Download)

2. 📦 **Descompacta o ficheiro ZIP** num diretório

3. ⚙️ **Edita os ficheiros de configuração**:

   * `OpenSim.ini` → configuração geral
   * `Regions/Regions.ini` → definir nome, posição e coordenadas da região

4. 🏁 **Executa o servidor**:

   ```bash
   mono OpenSim.exe        # No Linux/macOS com Mono
   OpenSim.exe             # No Windows
   ```

5. 📶 **Liga-te com um cliente** como o **Firestorm**:

   * URL: `http://localhost:9000` (modo standalone)
   * Criar uma conta de avatar no terminal do OpenSim na primeira execução

---

### 🧑‍💻 Comandos básicos no terminal do OpenSim:

| Comando       | Função                                            |
| ------------- | ------------------------------------------------- |
| `create user` | Cria um novo avatar                               |
| `show users`  | Mostra utilizadores online                        |
| `load oar`    | Carrega um ficheiro de região (paisagem, objetos) |
| `save oar`    | Guarda o estado da região atual                   |

---

### 🌐 Grid vs Standalone

| Modo           | Vantagens                       | Quando usar                                             |
| -------------- | ------------------------------- | ------------------------------------------------------- |
| **Standalone** | Fácil de configurar, tudo local | Testes, mundos pessoais                                 |
| **Grid**       | Escalável, servidores separados | Mundos partilhados, multi-utilizador, metaverso público |

---

### 📦 Ficheiros importantes:

* `OpenSim.ini` – configuração do servidor
* `Robust.HG.ini` – configuração do Robust Server
* `Regions/Regions.ini` – define as regiões do mundo
* `bin/` – onde está o executável do OpenSim
* `oar` – ficheiros de "scene" (como mapas salvos)

---

### 🧱 Exemplo de uma região (`Regions.ini`):

```ini
[MinhaRegiao]
RegionUUID = 00000000-0000-0000-0000-000000000000
Location = 1000,1000
InternalAddress = 0.0.0.0
InternalPort = 9000
AllowAlternatePorts = False
ExternalHostName = 127.0.0.1
```

---

### 🎨 O que podes criar no OpenSim?

* 🏰 Constrói edifícios, terrenos, mares, montanhas
* 🧍‍♂️ Avatares personalizados
* 🎮 Interações com scripts (Linden Scripting Language - LSL)
* 📦 Importa conteúdos do Second Life
* 🛰️ Liga-te a grids públicos como OSGrid

---

### 🎓 Conclusão

O **OpenSimulator** é uma plataforma poderosa e gratuita para criar o teu próprio **mundo virtual 3D**, seja para:

* **Ensino à distância**
* **Simulações de treino**
* **Jogos educativos**
* **Experiências artísticas**
* **Comunidades virtuais privadas**

---

### 📘 Se quiseres, posso ajudar com:

* Instalar o servidor no Windows ou Ubuntu
* Criar uma região com nome, terreno, avatar
* Usar um cliente 3D como Firestorm
* Fazer uma rede entre PCs com várias regiões
