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
---
Claro! Vamos desenvolver e **explicar em detalhe o OpenSimulator**, o **sistema de módulos** e **estrutura de ficheiros**, para que possas compreender como funciona por dentro e como podes personalizar ou expandir o teu mundo virtual.

---

## 🧠 O que é o OpenSim?

O **OpenSimulator (OpenSim)** é um **servidor de mundos 3D** que simula terrenos, avatares, objetos, interações, e permite ligações a clientes 3D como o **Firestorm**. Ele é modular e altamente configurável, sendo usado para fins educativos, sociais, de simulação e desenvolvimento.

---

## 📁 Estrutura de Ficheiros do OpenSimulator

Ao descompactar o OpenSim, vais encontrar algo como:

```
/opensim/
├── bin/                 # Ficheiros binários e DLLs (.NET)
│   ├── OpenSim.exe      # Executável principal do servidor
│   ├── Robust.exe       # Executável do Robust (modo Grid)
│   ├── OpenSim.ini      # Ficheiro de configuração principal
│   ├── Robust.*.ini     # Configurações do Robust
│   ├── Regions/         # Ficheiros de definição de regiões
│   ├── config-include/  # Inclui configurações adicionais
│   ├── OpenSim.Data.*   # Drivers de base de dados (SQLite, MySQL)
│   └── ScriptEngines/   # Scripts LSL compilados
├── doc/                 # Documentação
├── bin/oar-files/       # Ficheiros de backup das regiões
├── bin/assetcache/      # Cache de conteúdos
└── source/              # (se disponível) Código-fonte dos módulos
```

---

## 🔧 Sistema de Módulos no OpenSim

O OpenSim é **modular**, ou seja, funcionalidades como voz, física, mensagens, scripts, etc., são carregadas como **módulos dinâmicos (DLLs)**. Estes módulos são carregados com base na configuração e ficheiros `.ini`.

### 📌 Tipos de módulos

| Tipo de módulo                          | Função                                    |
| --------------------------------------- | ----------------------------------------- |
| **Serviços principais (Core Services)** | Inventário, avatares, utilizadores, login |
| **Região (Region Modules)**             | Scripts, colisões, physics, voz, chat     |
| **Módulos de comunicação**              | IM, ligações remotas, Hypergrid           |
| **Módulos de base de dados**            | SQLite, MySQL, PostgreSQL                 |
| **Módulos de script**                   | LSL (Linden Script Language), OSSL        |

---

## 🛠️ Exemplo: Como são configurados os módulos

### 📄 `OpenSim.ini`

Este ficheiro controla se módulos estão ativos ou não. Exemplo:

```ini
[Startup]
    ; Carregar módulos externos (DLLs)
    load_modules = true

[Modules]
    ; Ativar módulos específicos
    Include-Storage = "config-include/storage/MySQL.ini"
    Include-Scripting = "config-include/osslEnable.ini"
```

---

### 📄 `config-include` (subpastas)

Contém configurações específicas. Por exemplo:

* **`osslEnable.ini`** – ativa funcionalidades do **OpenSim Scripting Language (OSSL)** para scripts
* **`MySQL.ini`** – configura ligação à base de dados MySQL
* **`FlotsamCache.ini`** – configura cache de assets (texturas, scripts)

---

## ⚙️ Como os módulos funcionam

Os módulos são **carregados dinamicamente** no arranque do OpenSim, através das DLLs na pasta `bin/`.

Exemplo:

* Módulo `OpenSim.Region.ScriptEngine.Shared.dll` carrega o motor de scripts LSL
* Módulo `OpenSim.Region.OptionalModules.Avatar.Voice.Vivox.dll` adiciona suporte a voz Vivox

No ficheiro de configuração, podem ser ativados ou desativados:

```ini
[ScriptEngine]
    Enabled = true
    ScriptEngines = OpenSim.Region.ScriptEngine.XEngine.XEngine
```

---

## 💬 Scripts (LSL e OSSL)

OpenSim suporta **scripts LSL** (como no Second Life) e extensões **OSSL** com mais comandos, como:

```lsl
default
{
    state_entry()
    {
        llSay(0, "Olá mundo virtual!");
    }
}
```

* Os scripts são compilados e armazenados em `bin/ScriptEngines/` como ficheiros `.dll` para execução rápida.

---

## 🧱 Ficheiros de Regiões (`Regions/`)

Cada ficheiro `.ini` nesta pasta representa uma região do mundo.

### Exemplo: `Regiao1.ini`

```ini
[Regiao1]
RegionUUID = 3f37d015-f452-42b6-9df8-000000000001
Location = 1000,1000
InternalAddress = 0.0.0.0
InternalPort = 9000
ExternalHostName = 127.0.0.1
```

Podes definir várias regiões com diferentes nomes, posições no mapa e portas.

---

## 💾 Base de Dados

| Tipo       | Suporte               |
| ---------- | --------------------- |
| SQLite     | Simples, local        |
| MySQL      | Recomendado para Grid |
| PostgreSQL | (experimental)        |

OpenSim armazena:

* Contas de utilizadores
* Inventários
* Objetos criados
* Terrenos e assets

---

## 📚 Resumo

| Elemento         | Função                            |
| ---------------- | --------------------------------- |
| `OpenSim.exe`    | Servidor de simulação de região   |
| `Robust.exe`     | Servidor central de serviços      |
| `*.ini`          | Ficheiros de configuração modular |
| `ScriptEngines/` | Scripts compilados                |
| `Regions/*.ini`  | Definições das regiões do mundo   |
| `bin/*.dll`      | Módulos carregados dinamicamente  |

---

## 🧪 Queres um exemplo prático?

Posso criar:

* Uma configuração com 1 região
* Um módulo simples personalizado
* Um script `.lsl` para dar as boas-vindas aos visitantes
* Uma forma de adicionar novos módulos ao OpenSim

**criar um módulo personalizado** ou **instalar e configurar uma grid multi-região** ?

