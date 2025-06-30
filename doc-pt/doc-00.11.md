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
---
**explicar o OpenSimulator (OpenSim)** em 3 partes principais:

---

## 📌 1. O que é o OpenSimulator (servidor)

## 🎮 2. O Visualizador 3D (“Viewer”)

## 📁 3. O sistema de ficheiros e como tudo se organiza

---

## 📌 1. OpenSimulator – o servidor do mundo virtual

O **OpenSimulator** é o **servidor que simula o mundo virtual 3D**. Ele **não mostra o mundo graficamente** — apenas fornece os dados do mundo a clientes externos. É como o "motor" do metaverso.

### Principais funções:

* Controlar regiões (ilhas ou áreas do mundo)
* Gerir avatares (utilizadores)
* Armazenar terrenos, objetos, scripts, inventários
* Comunicar com os clientes via protocolo de rede (simulador → viewer)

### Modos de funcionamento:

| Modo                  | Descrição                                              |
| --------------------- | ------------------------------------------------------ |
| **Standalone**        | Tudo num só servidor, fácil de testar                  |
| **Grid (com Robust)** | Arquitetura distribuída, várias regiões, mais realista |

---

## 🎮 2. O Visualizador 3D ("Viewer")

O **Viewer** é o programa que o utilizador usa para **ver e interagir com o mundo virtual 3D**.

O OpenSim **não vem com um viewer** — é necessário usar um viewer externo compatível com o protocolo do Second Life, como:

### 🔸 Viewers compatíveis com OpenSim:

| Nome               | Descrição                                 |
| ------------------ | ----------------------------------------- |
| **Firestorm**      | O mais usado, potente, personalizável     |
| **Singularity**    | Leve, rápido, simples                     |
| **Cool VL Viewer** | Focado em performance e recursos técnicos |
| **Alchemy, Kokua** | Outras alternativas OpenSim-friendly      |

---

### 🔑 Como o viewer se liga ao OpenSim?

1. Inicia o viewer (ex: Firestorm)

2. Vai ao menu **"Preferências > OpenSim"** ou **"Grids"**

3. Adiciona a grid do teu servidor:

   * Nome: `Meu Mundo`
   * URI: `http://127.0.0.1:9000` (ou IP público)

4. Cria um utilizador no servidor com:

   ```
   create user nome apelido password email nome-regiao
   ```

5. Inicia sessão com esse utilizador no viewer.

---

### 🧭 Interface do viewer:

* **Avatar**: Podes personalizar (roupa, aspeto, etc.)
* **Inventário**: Itens, scripts, roupas, pastas
* **Terreno e construção**: Constrói, edita, move objetos
* **Chat local e IM**: Comunicação entre avatares
* **Mini-mapa e teleporte**: Navegação pelas regiões

---

## 📁 3. Sistema de ficheiros do OpenSim

A seguir, explico **como os ficheiros estão organizados** dentro do OpenSim (ex: versão zip extraída).

### 📂 Estrutura típica:

```
opensim/
├── bin/                      # Pasta principal
│   ├── OpenSim.exe           # Servidor da região
│   ├── Robust.exe            # Servidor central (Grid Mode)
│   ├── OpenSim.ini           # Configurações principais
│   ├── Robust.*.ini          # Configs do servidor robust
│   ├── config-include/       # Configurações adicionais
│   ├── Regions/              # Definições das regiões do mundo
│   ├── ScriptEngines/        # Scripts compilados (LSL/OSSL)
│   ├── oar-files/            # Backups de regiões (ficheiros OAR)
│   └── assetcache/           # Cache local de assets (texturas, objetos)
```

---

### 🧩 Ficheiros importantes:

| Ficheiro/Pasta    | Função                                                         |
| ----------------- | -------------------------------------------------------------- |
| `OpenSim.exe`     | Inicia a região                                                |
| `Robust.exe`      | Inicia os serviços de utilizador, login, inventário            |
| `OpenSim.ini`     | Configuração principal do simulador                            |
| `Robust.HG.ini`   | Configuração do Robust (modo grid com Hypergrid)               |
| `Regions/`        | Contém os ficheiros `.ini` de cada região                      |
| `config-include/` | Pastas com configurações de base de dados, scripts, permissões |
| `ScriptEngines/`  | Scripts LSL compilados em DLLs                                 |
| `*.oar`           | Ficheiros de cópia de segurança da região (paisagem, objetos)  |
| `*.iar`           | Backup do inventário de um utilizador                          |

---

### 📄 Exemplo de ficheiro de região (Regions/Regiao1.ini):

```ini
[Regiao1]
RegionUUID = 01234567-89ab-cdef-0123-456789abcdef
Location = 1000,1000
InternalPort = 9000
ExternalHostName = 127.0.0.1
```

---

### 💾 Base de dados

Pode ser:

* **SQLite** (padrão para testes)
* **MySQL/MariaDB** (recomendado para produção)

Armazena:

* Terrenos, objetos
* Utilizadores
* Inventários
* Scripts, grupos, assets

---

### 🗂 Exemplo de ficheiros salvos:

| Tipo             | Extensão | Conteúdo                            |
| ---------------- | -------- | ----------------------------------- |
| Região           | `.oar`   | Paisagem, terrenos, construções     |
| Inventário       | `.iar`   | Objetos e scripts de utilizador     |
| Scripts          | `.lsl`   | Código fonte antes de ser compilado |
| Script compilado | `.dll`   | Executado dentro do servidor        |

---

## 🎓 Conclusão geral

| Componente                   | Função                                                 |
| ---------------------------- | ------------------------------------------------------ |
| **OpenSim**                  | Servidor 3D do mundo virtual                           |
| **Viewer (Firestorm, etc.)** | Cliente gráfico para interagir com o mundo             |
| **Sistema de ficheiros**     | Armazena configurações, scripts, regiões, utilizadores |
| **Modularidade**             | Permite ativar/desativar módulos e funcionalidades     |

---

Um **viewer** (como o Firestorm), cria um **avatar**, ou montar uma **grid com múltiplas regiões**? 

* Uma forma de adicionar novos módulos ao OpenSim

**criar um módulo personalizado** ou **instalar e configurar uma grid multi-região** ?
Claro! Vamos desenvolver e **explicar passo a passo a instalação do OpenSimulator (OpenSim)** em **português europeu**, para que possas criar o teu próprio mundo virtual 3D — seja local (standalone) ou em rede (grid).

---

## 📦 O que vais instalar

* ✅ **OpenSimulator** (o servidor do mundo 3D)
* ✅ (opcional) **MySQL** (base de dados, melhor que SQLite)
* ✅ **Viewer 3D** (como Firestorm) para entrares no mundo

---

## 🖥️ Requisitos

| Recurso            | Mínimo recomendado                             |
| ------------------ | ---------------------------------------------- |
| Sistema operativo  | Windows 10 / Ubuntu / macOS (com Mono)         |
| CPU                | 2 núcleos ou mais                              |
| RAM                | 4 GB (8 GB para múltiplas regiões)             |
| Disco              | 2 GB livres ou mais                            |
| .NET / Mono        | .NET Framework (Windows) ou Mono (Linux/macOS) |
| Conexão à Internet | Opcional para uso local, necessário para grids |

---

## 📁 1. Fazer o download do OpenSim

1. Vai ao site oficial:

   * 🌐 [https://opensimulator.org/wiki/Download](https://opensimulator.org/wiki/Download)

2. Clica em **"Latest release"** (ex: `opensim-0.9.2.2.zip`)

3. Extrai o ficheiro ZIP para uma pasta à tua escolha, por exemplo:

   ```
   C:\OpenSim\
   ```

---

## ⚙️ 2. Configuração básica – Modo Standalone (servidor local)

1. Vai até à pasta `C:\OpenSim\bin`

2. Abre o ficheiro `OpenSim.ini` com um editor de texto (como Notepad++)

3. Certifica-te que estás em modo **Standalone**:

```ini
[Startup]
    ; Usa Standalone
    gridmode = false
```

4. Vai à subpasta `Regions\` e edita `Regions.ini`:

```ini
[MinhaRegiao]
RegionUUID = 00000000-0000-0000-0000-000000000000
Location = 1000,1000
InternalAddress = 0.0.0.0
InternalPort = 9000
ExternalHostName = 127.0.0.1
```

---

## 🏁 3. Executar o servidor

### No Windows:

1. Abre o terminal `cmd`
2. Vai até à pasta `C:\OpenSim\bin`
3. Escreve:

```cmd
OpenSim.exe
```

---

### No Ubuntu ou macOS (com Mono instalado):

```bash
cd ~/OpenSim/bin
mono OpenSim.exe
```

---

### Primeira execução:

* Ele vai pedir para criares um utilizador:

  ```
  First name: avatar
  Last name: teste
  Password: 1234
  E-mail: (opcional)
  Home region: MinhaRegiao
  ```

---

## 🔌 4. Instalar o Visualizador (Viewer)

1. Vai a [https://www.firestormviewer.org/downloads/](https://www.firestormviewer.org/downloads/)

2. Descarrega a versão **Firestorm para OpenSim**

3. Instala e abre o Firestorm

4. Vai a `Preferências > OpenSim` e adiciona a grid:

   * URI: `http://127.0.0.1:9000`
   * Nome: `LocalGrid`

5. Inicia sessão com o utilizador criado no OpenSim:

   * Nome: `avatar teste`
   * Password: `1234`

---

## 🧪 5. Testar o mundo virtual

* O teu avatar vai entrar numa ilha vazia
* Podes usar:

  * **Ctrl+B** para construir
  * **Inventário** (Ctrl+I) para adicionar objetos
  * **Scripts** para interação

---

## 💾 (Opcional) Usar MySQL em vez de SQLite

1. Instala MySQL (ou MariaDB)

2. Cria uma base de dados:

   ```sql
   CREATE DATABASE opensim CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
   CREATE USER 'opensim'@'localhost' IDENTIFIED BY 'minha_senha';
   GRANT ALL PRIVILEGES ON opensim.* TO 'opensim'@'localhost';
   ```

3. Abre `config-include\storage\MySQL.ini` e edita:

```ini
[MySqlDatabase]
    IncludeInStorage = true
    ConnectionString = Server=localhost;Database=opensim;User Id=opensim;Password=minha_senha;
```

4. No `OpenSim.ini`, ativa o uso do MySQL:

```ini
[DatabaseService]
    StorageProvider = "OpenSim.Data.MySQL.dll"
```

---

## 📚 Extras úteis

| Tarefa            | Comando                                          |
| ----------------- | ------------------------------------------------ |
| Criar novo avatar | `create user nome apelido password email regiao` |
| Guardar o mundo   | `save oar nome.oar`                              |
| Carregar um mundo | `load oar nome.oar`                              |
| Ver utilizadores  | `show users`                                     |

---

## ✅ Resumo

| Etapa                          | Estado |
| ------------------------------ | ------ |
| 🔽 Download do OpenSim         | ✅      |
| ⚙️ Configuração da região      | ✅      |
| 🏁 Execução do servidor        | ✅      |
| 🔍 Instalar viewer (Firestorm) | ✅      |
| 👤 Entrar com avatar           | ✅      |
| 🧱 Começar a construir         | ✅      |

---

## ❓ Queres agora:

* Configurar modo **Grid com Robust**?
* Adicionar **scripts e módulos personalizados**?
* Criar backup com `.oar` e partilhar com outros?
* Criar mundo em rede para ligares de outro PC?


