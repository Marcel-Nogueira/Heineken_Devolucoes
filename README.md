# 📋 Devoluções WhatsApp

Sistema web para gerenciar e compartilhar devoluções de produtos via WhatsApp.  
Lê dados diretamente de uma planilha Excel (.xlsm) — local ou via OneDrive.

**Autor:** Marcel H. Nogueira  
**Versão atual:** 3.1.0  
**Licença:** Uso interno LC Transportes

---

## 🚀 Como usar

### Opção 1 — GitHub Pages (recomendado)
Acesse diretamente pelo navegador em qualquer dispositivo:
```
https://SEU_USUARIO.github.io/REPOSITORIO/
```

### Opção 2 — Servidor local
1. Coloque `index.html` e `sw.js` na mesma pasta
2. Execute `INICIAR_SISTEMA.bat` (requer Python instalado)
3. Acesse `http://localhost:8765` no Chrome

### Opção 3 — Arquivo local (limitado)
Abra `index.html` diretamente no Chrome.  
⚠️ Sem sync automático — apenas visualização estática.

---

## 📁 Arquivos

| Arquivo | Descrição |
|---------|-----------|
| `index.html` | Sistema completo (único arquivo) |
| `sw.js` | Remove service workers antigos do navegador |
| `INICIAR_SISTEMA.bat` | Inicia servidor local no Windows |
| `README.md` | Esta documentação |

---

## ✨ Funcionalidades

- **Sync em tempo real** — detecta alterações na planilha a cada 1s (local) ou 15s (OneDrive)
- **Dois modos de conexão** — arquivo local ou OneDrive via Microsoft Graph API
- **Abas** — Todos os registros / Não Enviados (com badge de contagem)
- **Filtros** — por status, supervisor, motivo e texto livre
- **Grupos de Mesa** — configure o link de convite de cada grupo WhatsApp
- **Modal 2 passos** — Copiar mensagem → Abrir grupo (resolve limitação do WhatsApp)
- **Badges** — 🆕 Novo e ⏳ Não compartilhado por registro
- **Status colorido** — Devolução 🔴 / Aguardando 🔵 / Repasse 🟠 / Resolvido 🟢
- **Persistência** — grupos, itens enviados e sessão salvos no navegador

---

## ⚙️ Configurar Grupos de Mesa

1. Clique em **⚙️ Grupos de Mesa** no topo
2. Para cada mesa, cole o link de convite do grupo WhatsApp
3. Como obter o link: abra o grupo → **⋮ Mais → Link do grupo → Copiar link**
4. Formato: `https://chat.whatsapp.com/XXXXXXXXXXXXXX`

**Mesas padrão configuradas:**
32380, 32390, 32391, 32392, 32393, 32394, 32411, 32412, 32413, 32414, 32415, 32416


---

## 🔐 Configurar Azure AD (OneDrive login)

O app Azure AD já está registrado. Para funcionar corretamente, verifique:

### No portal.azure.com → App registrations → FreteDesk mini:

**1. Authentication → Add a platform → Single-page application**
```
Redirect URI: https://marcel-nogueira.github.io/Heineken_Devolucoes/
```
Adicione também para desenvolvimento local:
```
http://localhost:8765/index.html
```

**2. Supported account types**
Mude para: `Accounts in any organizational directory and personal Microsoft accounts`

**3. Application (client) ID** (já configurado no sistema)
```
a3241171-a3cb-41fc-890e-fe6ae363ed34
```

**4. Directory (tenant) ID** (já configurado no sistema)
```
a4ef2c0b-1b53-4b1e-902f-bd34cf9d1efb
```

---
## 📊 Estrutura da Planilha Excel

A planilha deve ter uma aba chamada **"Acompanhamento"** com as colunas:

| Col | Campo |
|-----|-------|
| A | DATA |
| D | MOTORISTA |
| E | Numero (telefone) |
| F | CATEGORIA (transportadora) |
| H | MESA |
| I | SETOR |
| J | DESCRIÇÃO (PDV) |
| L | SUPERVISOR |
| M | VENDEDOR |
| N | VALOR |
| P | MOTIVO |
| Q | OBSERVAÇÃO |
| R | STATUS |

A aba **"Tel Mot e Aju"** é usada para lookup de placa por motorista.

---

## 🔄 Deploy no GitHub Pages

1. Crie um repositório público no GitHub
2. Faça upload de `index.html` e `sw.js`
3. Vá em **Settings → Pages → Deploy from branch → main → Save**
4. Aguarde 2-5 minutos
5. Acesse: `https://SEU_USUARIO.github.io/REPOSITORIO/`

**Para atualizar:** substitua o `index.html` no repositório — o site atualiza automaticamente.

---

## 📦 Histórico de Versões

### v3.1.0 — 03/06/2026
- ✅ Client ID atualizado para app Azure AD registrado (`a3241171...`)
- ✅ Tenant ID configurado para o diretório correto
- ✅ Redirect URI válido para GitHub Pages

### v3.0.0 — 02/06/2026
- 🔧 **Reconstrução completa** do zero — sem patches acumulados
- ✅ **Fix definitivo dos botões** — todos os eventos via `addEventListener` (sem `onclick` inline)
- ✅ **Footer correto** dentro do card na tela inicial
- ✅ **Footer** com versão e copyright na tela principal
- ✅ **Arquivo nomeado** `index.html` para facilitar deploy no GitHub

### v2.9.0 — 02/06/2026
- Modal 2 passos: Copiar → Abrir Grupo (resolve texto sumindo no grupo)
- Fallback para `<input type=file>` quando aberto como arquivo local
- Footer com versão e copyright na tela de upload

### v2.8.0 — 02/06/2026
- MSAL.js popup para login Microsoft (funciona no GitHub Pages)
- Auto-restore de sessão OneDrive ao reabrir o sistema

### v2.7.0 — 02/06/2026
- Fix Client ID → Microsoft Graph Explorer (funciona de qualquer origem)
- Fix race condition clipboard + window.open

### v2.6.0 — 01/06/2026
- Abas **Todos** e **Não Enviados** com badge de notificação
- Copyright corrigido para Marcel H. Nogueira

### v2.5.0 — 30/05/2026
- Controle de versão implementado
- Modal "Sobre o sistema" com histórico
- Indicador de versão no rodapé

### v2.4.0 — 29/05/2026
- Tela de configuração de grupos de mesa
- 12 mesas padrão pré-carregadas
- Links de grupo salvos no navegador (persistência)

### v2.3.0 — 29/05/2026
- `sw.js` para limpar service workers antigos
- Campo para colar link de grupo por mesa
- Cópia automática da mensagem ao enviar

### v2.2.0 — 28/05/2026
- Layout em cards (eliminou bug da barra flutuante)
- Badge 🆕 Novo e ⏳ Não compartilhado
- Status colorido por tipo de devolução

### v2.1.0 — 28/05/2026
- Sync a cada 1 segundo (local)
- Detecção de alteração por tamanho + data do arquivo
- Exclusões sincronizadas

### v2.0.0 — 27/05/2026
- Dual source: Arquivo Local + OneDrive
- Login Microsoft via Device Code Flow
- Seletor de planilha do OneDrive

### v1.3.0 — 27/05/2026
- Campo Observação adicionado
- Filtro por Status da planilha
- Abertura direta no grupo da mesa

### v1.2.0 — 26/05/2026
- AutoSync com File System Access API
- Monitoramento a cada 5 segundos
- Filtros por supervisor e motivo

### v1.1.0 — 24/05/2026
- Versão HTML standalone com upload manual
- Prévia da mensagem antes de enviar
- Suporte a .xlsm e .xlsx

### v1.0.0 — 23/05/2026
- Versão inicial: botão WhatsApp na planilha Excel (.xlsm)
- Fórmula `=HYPERLINK()` com `ENCODEURL()`

---

## 🛠️ Tecnologias

- HTML5 / CSS3 / JavaScript vanilla
- [SheetJS (xlsx)](https://sheetjs.com/) — leitura de planilhas Excel
- [MSAL.js](https://github.com/AzureAD/microsoft-authentication-library-for-js) — autenticação Microsoft
- [Microsoft Graph API](https://graph.microsoft.com) — acesso ao OneDrive

---

*Marcel H. Nogueira © 2026*
