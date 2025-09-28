# 🚂 Deploy no Railway - RetechLog API Mock

Guia simples para fazer deploy da API Mock no Railway.

## 📋 Pré-requisitos

- Conta no [Railway](https://railway.app)
- Repositório no GitHub
- Node.js 20+ (para desenvolvimento local)

## 🚀 Deploy no Railway

### Opção 1: Deploy via GitHub (Recomendado)

1. **Conectar Repositório**
   - Acesse [Railway Dashboard](https://railway.app/dashboard)
   - Clique em "New Project"
   - Selecione "Deploy from GitHub repo"
   - Escolha o repositório `retechlog-api-mock`

2. **Configurar Variáveis de Ambiente**
   - No dashboard do projeto, vá em "Variables"
   - Adicione as variáveis do arquivo `env.railway`:
   ```bash
   NODE_ENV=production
   PORT=7272
   CORS_ALLOWED_ORIGINS=http://localhost:8082,http://localhost:3000,https://retechlog-ui.vercel.app
   JWT_SECRET=sua-chave-jwt-secreta-aqui
   JWT_EXPIRES_IN=7d
   LOG_LEVEL=info
   MOCK_DELAY_MIN=100
   MOCK_DELAY_MAX=500
   ```

3. **Deploy Automático**
   - Railway detectará automaticamente o `railway.json`
   - Usará o `Dockerfile.railway` para build
   - Deploy será feito automaticamente

### Opção 2: Deploy via Railway CLI

```bash
# Instalar Railway CLI
npm install -g @railway/cli

# Login no Railway
railway login

# Inicializar projeto
railway init

# Adicionar variáveis de ambiente
railway variables set NODE_ENV=production
railway variables set JWT_SECRET=sua-chave-jwt-secreta
railway variables set CORS_ALLOWED_ORIGINS=http://localhost:8082,http://localhost:3000

# Deploy
railway up
```

## 🔧 Configuração

### Variáveis de Ambiente Importantes

```bash
# Obrigatórias
NODE_ENV=production
JWT_SECRET=sua-chave-jwt-forte-min-32-caracteres

# CORS - Ajustar conforme seu frontend
CORS_ALLOWED_ORIGINS=http://localhost:8082,http://localhost:3000,https://seu-frontend.vercel.app

# Opcionais
LOG_LEVEL=info
MOCK_DELAY_MIN=100
MOCK_DELAY_MAX=500
MOCK_ERROR_RATE=0.02
```

### Domínio Customizado (Opcional)

1. No dashboard do Railway, vá em "Settings"
2. Clique em "Custom Domain"
3. Adicione seu domínio (ex: `api-mock.retechlog.com`)
4. Configure DNS conforme instruções

## ✅ Verificação do Deploy

### 1. Health Check
```bash
curl https://seu-projeto.up.railway.app/api/health
```

### 2. Teste de Endpoints
```bash
# Testar produtos
curl https://seu-projeto.up.railway.app/api/product/list

# Testar autenticação
curl -X POST https://seu-projeto.up.railway.app/api/auth/sign-in \
  -H "Content-Type: application/json" \
  -d '{"email":"test@example.com","password":"password"}'

# Testar CORS
curl -H "Origin: http://localhost:8082" \
     -H "Access-Control-Request-Method: GET" \
     -X OPTIONS \
     https://seu-projeto.up.railway.app/api/product/list
```

## 🔗 Conectar Frontend

### Variável de Ambiente no Frontend

```bash
# No seu projeto retechlog-ui
NEXT_PUBLIC_SERVER_URL=https://seu-projeto.up.railway.app
```

### Exemplo de uso no código:

```typescript
// src/lib/api.ts
const API_BASE_URL = process.env.NEXT_PUBLIC_SERVER_URL || 'http://localhost:7272';

export const api = {
  products: {
    list: () => fetch(`${API_BASE_URL}/api/product/list`),
    details: (id: string) => fetch(`${API_BASE_URL}/api/product/details?productId=${id}`)
  },
  auth: {
    signIn: (credentials: any) => fetch(`${API_BASE_URL}/api/auth/sign-in`, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(credentials)
    })
  }
};
```

## 📊 Monitoramento

### Logs no Railway
- Acesse o dashboard do projeto
- Vá em "Deployments" → Clique no deploy ativo
- Veja logs em tempo real na aba "Logs"

### Métricas Básicas
- Railway fornece métricas básicas de CPU e memória
- Logs estruturados para debugging

## 🔄 Atualizações

### Deploy Automático
- Push para `main` branch = deploy automático
- Railway detecta mudanças e faz rebuild

### Deploy Manual
```bash
# Via CLI
railway up

# Via Dashboard
- Clique em "Redeploy" no dashboard
```

## 💰 Custos

### Plano Gratuito
- ✅ 500 horas/mês de execução
- ✅ 1GB RAM
- ✅ 1 vCPU
- ✅ Domínio `.up.railway.app`

### Plano Pro ($5/mês)
- ✅ Execução ilimitada
- ✅ 8GB RAM
- ✅ 8 vCPU
- ✅ Domínio customizado
- ✅ SSL automático

## 🚨 Troubleshooting

### Problemas Comuns

1. **Build Failed**
   ```bash
   # Verificar logs no dashboard
   # Verificar se todas as dependências estão no package.json
   ```

2. **CORS Issues**
   ```bash
   # Verificar CORS_ALLOWED_ORIGINS
   railway variables set CORS_ALLOWED_ORIGINS=https://seu-frontend.vercel.app
   ```

3. **Port Issues**
   ```bash
   # Railway usa PORT dinâmico, verificar se está configurado
   railway variables set PORT=7272
   ```

### Logs Úteis

```bash
# Ver logs via CLI
railway logs

# Ver logs específicos
railway logs --tail 100
```

## 🎯 URLs de Exemplo

Após o deploy, sua API estará disponível em:
- **Railway URL**: `https://retechlog-api-mock-production-xxxx.up.railway.app`
- **Domínio customizado**: `https://api-mock.retechlog.com` (se configurado)

### Endpoints Disponíveis:
- `GET /api/health` - Health check
- `GET /api/product/list` - Lista de produtos
- `POST /api/auth/sign-in` - Login
- `GET /api/calendar` - Eventos do calendário
- `GET /api/kanban` - Board Kanban
- E muitos outros...

---

**Deploy realizado com sucesso!** 🎉

Sua API Mock está pronta para conectar com o frontend!
