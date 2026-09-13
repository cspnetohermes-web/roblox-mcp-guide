# 🎮 Roblox Studio + Hermes MCP — Guia Completo

> Aprenda a conectar o Roblox Studio ao Hermes Agent via MCP (Model Context Protocol) e editar seus jogos usando IA!

---

## 📋 Índice

1. [O que é MCP?](#o-que-é-mcp)
2. [Pré-requisitos](#pré-requisitos)
3. [Passo 1: Ativar o Servidor MCP no Roblox Studio](#passo-1-ativar-o-servidor-mcp-no-roblox-studio)
4. [Passo 2: Configurar o Hermes](#passo-2-configurar-o-hermes)
5. [Passo 3: Reiniciar o Hermes](#passo-3-reiniciar-o-hermes)
6. [Passo 4: Verificar a Conexão](#passo-4-verificar-a-conexão)
7. [Ferramentas Disponíveis](#ferramentas-disponíveis)
8. [Exemplos Práticos](#exemplos-práticos)
9. [Solução de Problemas](#solução-de-problemas)

---

## O que é MCP?

MCP (Model Context Protocol) é um protocolo que permite que agentes de IA (como o Hermes) se conectem a ferramentas externas — no caso, o Roblox Studio.

Com isso, você pode:
- ✅ Criar objetos no Workspace via código Luau
- ✅ Editar scripts existentes
- ✅ Executar comandos no Command Bar
- ✅ Buscar assets do Creator Store
- ✅ Gerar meshes e texturas com IA
- ✅ Controlar playtests

---

## Pré-requisitos

| Item | Versão mínima |
|------|---------------|
| **Roblox Studio** | Build 0.738+ (MCP embutido) |
| **Hermes Agent** | Última versão |
| **Windows 10/11** | Qualquer versão recente |
| **macOS** | 12+ (Monterey ou superior) |

> ⚠️ Funciona tanto no **Windows** quanto no **macOS**! Os comandos para cada sistema estão indicados abaixo.

---

## Passo 1: Ativar o Servidor MCP no Roblox Studio

1. Abra o **Roblox Studio**
2. Abra um lugar (File → New ou abra um existente)
3. Vá no menu **Assistant** (barra lateral direita)
4. Clique em **⋯** (três pontos) → **Manage MCP Servers**
5. Ligue a opção: **Enable Studio as MCP server**
6. Deve aparecer **"1 client connected"** no canto inferior direito

> **Importante:** O servidor MCP só funciona com o lugar **aberto no Edit Mode** (não no Play Mode).

---

## Passo 2: Configurar o Hermes

Abra o arquivo de configuração do Hermes:

```bash
~/.hermes/config.yaml
```

Adicione a seguinte configuração (escolha de acordo com seu sistema):

### macOS

```yaml
mcp_servers:
  Roblox_Studio:
    command: /Applications/RobloxStudio.app/Contents/MacOS/StudioMCP
```

### Windows

```yaml
mcp_servers:
  Roblox_Studio:
    command: cmd.exe
    args: ["/c", "%LOCALAPPDATA%\\Roblox\\mcp.bat"]
```

> **Dica:** No Windows, o `mcp.bat` fica na pasta `%LOCALAPPDATA%\Roblox\`. Se não existir, crie um arquivo de texto com o conteúdo:
> ```
> @echo off
> "%~dp0RobloxStudioBeta.exe" -MCP
> ```

---

## Passo 3: Reiniciar o Hermes

Após editar o `config.yaml`, **reinicie o Hermes** para carregar a nova configuração:

1. Feche o app do Hermes
2. Abra novamente
3. O Hermes deve detectar automaticamente o servidor MCP

---

## Passo 4: Verificar a Conexão

No Hermes, pergunte: *"Quais ferramentas MCP estão disponíveis?"*

Você deve ver ferramentas como:
- `mcp__Roblox_Studio__execute_luau`
- `mcp__Roblox_Studio__search_game_tree`
- `mcp__Roblox_Studio__inspect_instance`
- `mcp__Roblox_Studio__script_read`
- `mcp__Roblox_Studio__multi_edit`
- `mcp__Roblox_Studio__search_asset`
- `mcp__Roblox_Studio__insert_asset`
- `mcp__Roblox_Studio__start_stop_play`
- `mcp__Roblox_Studio__screen_capture`
- `mcp__Roblox_Studio__get_studio_state`
- `mcp__Roblox_Studio__list_roblox_studios`

---

## Ferramentas Disponíveis

### 🔧 Manipulação do Jogo

| Ferramenta | Descrição |
|------------|-----------|
| `execute_luau` | Executa código Luau no Studio (Edit Mode) |
| `search_game_tree` | Explora a hierarquia do jogo |
| `inspect_instance` | Mostra propriedades de um objeto |
| `script_read` | Lê o conteúdo de um script |
| `multi_edit` | Faz múltiplas edições em um script |
| `script_search` | Busca texto em todos os scripts |

### 🎮 Playtest

| Ferramenta | Descrição |
|------------|-----------|
| `start_stop_play` | Inicia/para o playtest |
| `screen_capture` | Captura tela do Studio |
| `user_keyboard_input` | Simula teclado |
| `user_mouse_input` | Simula mouse |

### 🎨 Assets e Criação

| Ferramenta | Descrição |
|------------|-----------|
| `search_asset` | Busca assets no Creator Store |
| `insert_asset` | Insere um asset no jogo |
| `generate_mesh` | Gera mesh com IA |
| `generate_texture` | Gera textura com IA |
| `generate_material` | Gera material com IA |
| `generate_procedural_model` | Cria modelos procedurais |

---

## Exemplos Práticos

### 1. Criando uma Parte Simples

**Prompt para o Hermes:**
```
Crie uma parte vermelha no Workspace chamada "Plataforma" com tamanho 10, 1, 10 na posição 0, 0, 0
```

**Código Luau gerado:**
```lua
local part = Instance.new("Part")
part.Name = "Plataforma"
part.Size = Vector3.new(10, 1, 10)
part.Position = Vector3.new(0, 0, 0)
part.Color = Color3.fromRGB(255, 0, 0)
part.Anchored = true
part.Parent = workspace
```

### 2. Criando uma Casa Completa

**Prompt:**
```
Crie uma casa simples com paredes, telhado, porta e janela
```

### 3. Explorando o Workspace

**Prompt:**
```
Mostre-me a hierarquia do Workspace
```

### 4. Inserindo um Asset do Creator Store

**Prompt:**
```
Insira o asset de ID 10177764079 no Workspace
```

### 5. Executando Código Luau

**Prompt:**
```
Execute este código no Studio:
print("Olá do Hermes!")
```

---

## Solução de Problemas

### ❌ "MCP server unreachable"

**Causa:** O Roblox Studio não está com o MCP ativado.

**Solução:**
1. Verifique se o lugar está aberto no **Edit Mode**
2. Vá em **Assistant → ⋯ → Manage MCP Servers**
3. Ligue **Enable Studio as MCP server**
4. Reinicie o Hermes

### ❌ "Edit datamodel is not available in Play mode"

**Causa:** Você está tentando editar enquanto o jogo está rodando.

**Solução:** Pare o playtest antes de editar (use `start_stop_play` com `is_start: false`)

### ❌ "StudioMCP not found"

**Causa:** O Roblox Studio está desatualizado.

**Solução:** Atualize o Roblox Studio para a versão mais recente.

### ❌ "1 client connected" não aparece

**Solução:**
1. Feche o Roblox Studio completamente
2. Reabra o lugar
3. Reative o MCP
4. Reinicie o Hermes

---

## 💡 Dicas

1. **Sempre use `datamodel_type: "Edit"`** no `execute_luau` para editar o jogo
2. **Pare o playtest** antes de fazer alterações estruturais
3. **Use `search_game_tree`** para entender a estrutura do seu lugar
4. **Combine ferramentas:** use `search_asset` + `insert_asset` para adicionar models prontos
5. **Teste no Play Mode** use `start_stop_play` com `is_start: true`

---

## 🔗 Links Úteis

- [Roblox Studio Download](https://create.roblox.com)
- [Hermes Agent](https://hermes-agent.nousresearch.com)
- [Documentação MCP](https://modelcontextprotocol.io)
- [Creator Store](https://create.roblox.com/store)

---

## 📝 Notas

- O MCP do Roblox Studio usa transporte **stdio** (comunicação via terminal)
- O servidor MCP é embutido no Roblox Studio (não é um plugin externo)
- Funciona no **macOS** e **Windows**
- O Hermes precisa ser reiniciado após mudanças no `config.yaml`
- No Windows, se o `mcp.bat` não existir, crie-o manualmente na pasta `%LOCALAPPDATA%\Roblox\`

---

**Criado por:** Carlos Neto (Neto)  
**Última atualização:** 2026
