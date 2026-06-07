# VRTX Agency — Site Teste

Site Fictício de agência de Marketing integrado ao agente de atendimento 
Luna via backend Node.js + Groq API.

## Estrutura

index.html   ← site completo (single file)
README.md

## Como funciona o chat

O chat do site conecta diretamente à rota /chat do backend:

- Backend: Node.js + Express rodando no Oracle Cloud
- IA: Groq API com modelo llama-3.3-70b-versatile
- Tunnel: ngrok (URL fixa permanente)
- Sessão: sessionId persistido no localStorage do navegador
- TTL: Sessões expiram após 2h de inatividade no servidor
- CORS: configurado no backend (origin: *)

## Telegram

- Bot: @agente_marketing_sette_bot
- Webhook: https://alienate-lively-budget.ngrok-free.dev/telegram
- O mesmo agente Luna atende tanto pelo chat do site quanto pelo Telegram
- Ao finalizar o briefing, uma notificação é enviada automaticamente 
  para o Telegram pessoal do administrador
- Comando /start reinicia a conversa no Telegram

## URL do backend

const BACKEND_URL = 'https://alienate-lively-budget.ngrok-free.dev';

## Deploy

Site publicado via Vercel com deploy automático a partir desta branch.

## Backend — comandos úteis

# Ver status dos processos
pm2 status

# Ver logs do agente
pm2 logs agente-telegram --lines 30

# Reiniciar agente
pm2 restart agente-telegram --update-env

# Ver sessões ativas
curl https://alienate-lively-budget.ngrok-free.dev/health

# Reiniciar tunnel ngrok
pm2 restart ngrok-tunnel
