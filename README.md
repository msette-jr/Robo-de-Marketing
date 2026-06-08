# VRTX Agency — Site Modelo

Site modelo de Agência de Markenting integrado ao agente de atendimento
Luna via backend Node.js + Anthropic API (Claude Haiku 4.5).

## Estrutura

index.html   ← site completo (single file)
README.md

## Como funciona o chat

O chat do site conecta diretamente à rota /chat do backend:

- Backend: Node.js + Express rodando no Oracle Cloud ARM
- IA: Anthropic API — Claude Haiku 4.5
- Tunnel: ngrok (domínio fixo permanente)
- Sessão: sessionId persistido no localStorage do navegador
- TTL: Sessões expiram após 2h de inatividade no servidor
- CORS: configurado no backend (origin: *)
- Tokens: limite baseado no saldo Anthropic (~8M tokens / US$ 7,98)

## Telegram

- Bot: @agente_marketing_sette_bot
- Webhook: https://alienate-lively-budget.ngrok-free.dev/telegram
- O mesmo agente Luna atende tanto pelo chat do site quanto pelo Telegram
- A cada pergunta, Luna oferece sugestões criativas adaptadas ao contexto
- Ao finalizar o briefing, uma notificação é enviada automaticamente
  para o Telegram pessoal do administrador
- Comando /start reinicia a conversa no Telegram

## URL do backend

const BACKEND_URL = 'https://alienate-lively-budget.ngrok-free.dev';

## Deploy

Site publicado via Vercel com deploy automático a partir desta branch.

## Contato & Automações

- Email: msettejr@outlook.com
- GitHub: https://github.com/msette-jr

## Backend — comandos úteis

# Ver status dos processos
pm2 status

# Ver logs do agente
pm2 logs agente-telegram --lines 30

# Reiniciar agente
pm2 restart agente-telegram --update-env

# Ver sessões e tokens do dia
curl https://alienate-lively-budget.ngrok-free.dev/health

# Reiniciar tunnel ngrok
pm2 restart ngrok-tunnel

# Atualizar tokens manualmente
echo '{"date":"YYYY-MM-DD","tokens":0}' > ~/agente-telegram/daily-tokens.json
