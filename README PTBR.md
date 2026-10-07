# ⚠️💾 NETWORK VIRUS IDENTIFIER PORTABLE

Esse projeto ajuda a identificar e detectar softwares maliciosos na máquina. Para contribuir com a comunidade, ele foi portado para um executável, deixando-o mais acessível para técnicos e pessoas com bom conhecimento em informática usarem no dia a dia de trabalho.

O monitor mostra, em tempo real, quais programas do computador estão se comunicando com a internet, para qual IP e a partir de qual pasta o programa está rodando.

> English version: [README.md](README.md)

---

# Terminal

<img width="1674" height="989" alt="Captura de tela 2026-03-13 112215" src="https://github.com/user-attachments/assets/2c4cb8d1-4846-4bd9-bd26-267bac2842a1" />

---

# Como instalar?

1. Acesse a aba **Releases** deste repositório.
2. Baixe o arquivo **`NetworkVirusIdentifier.exe`**.
3. Salve em qualquer pasta (ou em um pendrive, já que é portátil).
4. Dê duplo clique para abrir e aceite a solicitação de administrador (UAC).

Pronto, o monitor já começa a exibir as conexões.

> Para fechar, basta fechar a janela ou pressionar `Ctrl + C`.

---

# Requisitos

- Windows 10 ou superior (64 bits)
- Permissão de **administrador**

> O programa usa `netstat` e PowerShell, que já vêm no Windows. A versão para Linux está nos planos para uma próxima atualização.

---

#  Entendendo a tela

### `[ CONNECTIONS ESTABLISHED ]`

| Coluna | Significado |
|---|---|
| `PROCESS` | Nome do programa que abriu a conexão |
| `PID` | Identificador do processo no Windows |
| `REMOTE_IP` | IP do destino |
| `STATUS` | Estado da conexão (`ESTABLISHED`) |
| `PATH` | Pasta onde o executável está salvo |

### `[ LATEST DISCONNECTIONS ]`

Histórico das conexões que foram encerradas (guarda as últimas 200), com o processo, o IP e o horário (`CLOSED_AT`).

### 🚩 Sinais de alerta

Ao analisar a lista, fique atento a:

- Programas rodando de pastas incomuns, como `AppData\Local\Temp`, `Downloads` ou `ProgramData`
- Nomes parecidos com processos do Windows, mas em local errado (por exemplo, um `svchost.exe` fora de `C:\Windows\System32`)
- Conexões constantes para IPs desconhecidos
- Processos com `PATH` igual a `RESTRICTED ACCESS` (rode como administrador para ver o caminho)

> Uma conexão suspeita não significa necessariamente que existe um vírus. Pesquise o IP e o programa antes de tomar qualquer decisão.

---

#  Aviso sobre antivírus

Por ser um executável que chama PowerShell e `netstat`, o Windows Defender e outros antivírus podem marcá-lo como falso positivo. O código-fonte é aberto e está neste repositório, então você pode revisá-lo ou gerar o seu próprio executável (veja abaixo).

---

#  Como gerar o executável (para desenvolvedores)

O projeto usa o **Node SEA** (Single Executable Applications) para empacotar o código.

### Pré-requisitos

- [Node.js 20 ou superior](https://nodejs.org)

### Passo a passo

```bash
# 1. Clone o repositório
git clone https://github.com/Shazanxz/Network-Virus-Identifier-Portable.git
cd Network-Virus-Identifier

# 2. Instale as dependências
npm install

# 3. Gere o executável
npm run build
```

O resultado fica em `build/NetworkVirusIdentifier.exe`.

### Rodando sem gerar o executável

```bash
node index.js
```

### Estrutura do projeto

```
Network-Virus-Identifier/
├── assets/
│   └── logo.ico        # ícone do executável
├── build/              # executável final (gerado)
├── dist/               # arquivos intermediários (gerado)
├── index.js            # código do monitor
├── build-sea.js        # script que gera o executável
├── sea-config.json     # configuração do Node SEA
└── package.json
```

# Créditos

- **devbluen** - Criador do projeto
- **Shazanxz** - Port para Executavel

Se este projeto te ajudou, deixe uma ⭐ no repositório e mantenha os créditos ao redistribuir.