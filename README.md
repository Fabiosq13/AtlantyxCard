# Atlantyx Sender · Deploy no Vercel

Landing page do Sender Kit com URLs limpas para one-pagers e agenda.

## O que este projeto faz

Depois do deploy, você terá estas URLs:

| URL | O que faz |
|-----|-----------|
| `/` | Painel de controle (seu "app" no celular) |
| `/pt` | Abre o one-pager em Português (PDF) |
| `/en` | Abre o one-pager em English (PDF) |
| `/meet` | Redireciona para seu Calendly |
| `/linkedin` | Redireciona para seu LinkedIn |
| `/site` | Redireciona para atlantyx.io |

Preview automático no WhatsApp (Open Graph image) quando alguém receber o link.

---

## Deploy passo-a-passo (escolha uma das 3 opções)

### Opção 1 — Drag & drop (mais rápido, 2 minutos)

1. Vá em **[vercel.com/new](https://vercel.com/new)**
2. Clique em **"Deploy without Git"** (canto inferior)
3. Arraste a pasta inteira `atlantyx-vercel-deploy` para a janela
4. Dá nome ao projeto: `atlantyx-sender` (ou outro nome curto)
5. Clique **Deploy**
6. Pronto. Você terá uma URL tipo `atlantyx-sender.vercel.app`

### Opção 2 — Via GitHub (recomendada, permite updates fáceis)

1. Crie um repositório novo no GitHub (pode ser privado): `atlantyx-sender`
2. Faça upload dos arquivos da pasta para o repo (pela interface web do GitHub ou via `git push`)
3. Vá em **[vercel.com/new](https://vercel.com/new)**
4. Clique em **"Import Git Repository"** → selecione `atlantyx-sender`
5. Framework preset: **Other** (não mexe em nada)
6. Clique **Deploy**
7. Depois disso, qualquer commit no GitHub faz deploy automático

### Opção 3 — CLI (para desenvolvedores)

```bash
cd atlantyx-vercel-deploy
npm install -g vercel
vercel
# Segue as perguntas interativas. Confirma projeto novo: atlantyx-sender
# Depois: vercel --prod (para subir em produção)
```

---

## Testando depois do deploy

Abre no celular (ou desktop):

- `https://SEU-PROJETO.vercel.app/` → painel de controle
- `https://SEU-PROJETO.vercel.app/pt` → abre PDF PT
- `https://SEU-PROJETO.vercel.app/en` → abre PDF EN
- `https://SEU-PROJETO.vercel.app/meet` → redireciona Calendly

Testa também colando o link num WhatsApp → deve aparecer preview com logo Atlantyx.

---

## Adicionar à tela inicial do Android (vira "app")

1. Abre `https://SEU-PROJETO.vercel.app/` no **Chrome** do celular
2. Menu ⋮ → **"Adicionar à tela inicial"**
3. Confirma — ícone preto com logo Atlantyx aparece na home
4. Toca nele: abre em modo fullscreen, parece um app nativo

---

## Domínio próprio (opcional, super-premium)

Se você tem o domínio **atlantyx.io**, pode apontar um subdomínio:

1. No painel Vercel → Settings → Domains
2. Adicione: `go.atlantyx.io` ou `sender.atlantyx.io`
3. No seu provedor de DNS (registro.br, GoDaddy, etc), cria registro CNAME:
   ```
   Type: CNAME
   Host: go
   Value: cname.vercel-dns.com
   ```
4. Aguarda propagar (10 min a 1 hora)
5. Agora seus links ficam `go.atlantyx.io/pt` — bem mais profissional

---

## Atualizar os PDFs depois

Você fez v2 da one-page? Só substitui os arquivos em `/public/` e redeploya:

- `public/atlantyx-onepage-pt.pdf` ← versão em PT
- `public/atlantyx-onepage-en.pdf` ← versão em EN

Commit no GitHub (se usou opção 2) e Vercel redeploya em 30 segundos. **URL não muda** — os QR codes e links já distribuídos continuam funcionando.

---

## Estrutura dos arquivos

```
atlantyx-vercel-deploy/
├── public/
│   ├── index.html                     # painel de controle
│   ├── atlantyx-onepage-pt.pdf        # one-page PT
│   ├── atlantyx-onepage-en.pdf        # one-page EN
│   ├── og-image.png                   # preview WhatsApp (1200x630)
│   ├── apple-icon.png                 # ícone iOS
│   ├── favicon.png                    # ícone browser
│   └── icon.png                       # logo Atlantyx preto
├── vercel.json                        # configuração rotas
└── README.md                          # este arquivo
```

---

## Regerar os QR cards com a URL Vercel

Depois do deploy, atualize os QRs para que apontem para a URL Vercel (em vez do wa.me direto). Isso permite rastrear cliques no futuro e trocar o destino sem refazer o QR.

Use **qrfy.com** (grátis):
- QR PT → gera com URL: `https://SEU-PROJETO.vercel.app/pt`
- QR EN → gera com URL: `https://SEU-PROJETO.vercel.app/en`

Ou, se quiser manter o QR abrindo WhatsApp (fluxo Cenário B do guia), continue usando:
- `https://wa.me/5521960153911?text=MENSAGEM_ENCODED`

Os cartões `Atlantyx_QRcard_PT.png` e `Atlantyx_QRcard_EN.png` atuais já vão estar corretos para o fluxo B (cliente → WhatsApp seu).

---

## Suporte

Qualquer problema no deploy, Vercel tem docs excelente em [vercel.com/docs](https://vercel.com/docs).
