# VRTX Agency — Site Institucional

Site institucional da VRTX Agency integrado ao agente de atendimento Luna via backend Node.js + Groq.

## Estrutura

```
agencia-marketing.html   ← site completo (single file)
README.md
```

## Como funciona o chat

O chat do site conecta diretamente à rota `/chat` do backend:

- **Backend:** Node.js + Express rodando no Oracle Cloud
- **IA:** Groq API com modelo `llama-3.3-70b-versatile`
- **Tunnel:** Cloudflare Tunnel (expõe o backend publicamente)
- **Sessão:** `sessionId` persistido no `localStorage` do navegador
- **TTL:** Sessões expiram após 2h de inatividade no servidor

## Configuração

Antes de publicar, atualize a URL do backend no HTML:

```js
const BACKEND_URL = 'https://alienate-lively-budget.ngrok-free.dev';
```

## CORS — obrigatório no backend

Para o site em produção (GitHub Pages ou outro host) funcionar,
adicione o domínio do site no `server.js`:

```js
import cors from 'cors';
app.use(cors({ origin: 'https://seu-usuario.github.io' }));
```

Instale o pacote:
```bash
npm install cors
cd ~/agente-telegram && npm install cors
```

## Deploy no GitHub Pages

1. Crie um repositório público no GitHub
2. Suba o `agencia-marketing.html` e o `README.md`
3. Vá em **Settings → Pages → Deploy from branch → main**
4. O site ficará em: `https://seu-usuario.github.io/nome-do-repo/agencia-marketing.html`

## Backend — comandos úteis

```bash
# Ver status
pm2 status

# Ver logs
pm2 logs agente-telegram --lines 30

# Reiniciar
pm2 restart agente-telegram --update-env

# Ver sessões ativas
curl https://alienate-lively-budget.ngrok-free.dev/health
```
