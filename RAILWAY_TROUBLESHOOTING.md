# 🚨 Troubleshooting Railway - RetechLog API Mock

## Problema: `/bin/sh: next: not found`

### ✅ Solução Aplicada

1. **Dockerfile Simplificado**: Criado `Dockerfile.railway.simple` mais simples
2. **Script Start Corrigido**: Removido `-p 7272` do script start
3. **Porta Dinâmica**: Railway define automaticamente a porta

### 🔧 Mudanças Realizadas

#### 1. `railway.json` atualizado:
```json
{
  "build": {
    "builder": "DOCKERFILE",
    "dockerfilePath": "Dockerfile.railway.simple"
  },
  "deploy": {
    "startCommand": "yarn start"
  }
}
```

#### 2. `package.json` corrigido:
```json
{
  "scripts": {
    "start": "next start"  // Removido -p 7272
  }
}
```

#### 3. `Dockerfile.railway.simple` criado:
```dockerfile
FROM node:20-alpine
WORKDIR /app
COPY package.json yarn.lock* ./
RUN yarn install --frozen-lockfile
COPY . .
ENV NODE_ENV production
RUN yarn build
EXPOSE $PORT
CMD ["yarn", "start"]
```

## 🚀 Próximos Passos

### 1. Fazer Commit das Mudanças
```bash
git add .
git commit -m "fix: corrigir deploy Railway - next command not found"
git push origin main
```

### 2. Redeploy no Railway
- O Railway fará deploy automático após o push
- Ou clique em "Redeploy" no dashboard

### 3. Verificar Logs
- No dashboard Railway, vá em "Deployments"
- Clique no deploy ativo
- Verifique a aba "Logs"

## ✅ Verificação do Deploy

### Health Check
```bash
curl https://seu-projeto.up.railway.app/api/health
```

### Teste de Endpoints
```bash
# Testar produtos
curl https://seu-projeto.up.railway.app/api/product/list

# Testar autenticação
curl -X POST https://seu-projeto.up.railway.app/api/auth/sign-in \
  -H "Content-Type: application/json" \
  -d '{"email":"test@example.com","password":"password"}'
```

## 🔍 Outros Problemas Comuns

### 1. Build Failed
```bash
# Verificar se todas as dependências estão no package.json
# Verificar logs de build no Railway dashboard
```

### 2. CORS Issues
```bash
# Verificar CORS_ALLOWED_ORIGINS
railway variables set CORS_ALLOWED_ORIGINS=https://seu-frontend.vercel.app
```

### 3. Port Issues
```bash
# NÃO configure PORT manualmente
# Railway define automaticamente via $PORT
```

### 4. Memory Issues
```bash
# Verificar uso de memória no dashboard
# Considerar upgrade do plano se necessário
```

## 📊 Logs Úteis

### Comandos para Debug
```bash
# Ver logs via CLI
railway logs

# Ver logs específicos
railway logs --tail 100

# Ver logs de build
railway logs --build
```

### Logs Importantes no Dashboard
- **Build logs**: Verificar se o build foi bem-sucedido
- **Runtime logs**: Verificar se a aplicação está rodando
- **Error logs**: Verificar erros específicos

## 🎯 Checklist de Deploy

- [ ] ✅ `railway.json` configurado corretamente
- [ ] ✅ `Dockerfile.railway.simple` criado
- [ ] ✅ `package.json` script start corrigido
- [ ] ✅ Variáveis de ambiente configuradas (SEM PORT)
- [ ] ✅ Commit e push realizados
- [ ] ✅ Deploy automático ou manual executado
- [ ] ✅ Health check funcionando
- [ ] ✅ Endpoints testados

## 🚀 Deploy Bem-sucedido

Após corrigir esses problemas, sua API Mock estará rodando em:
- **URL**: `https://seu-projeto.up.railway.app`
- **Health**: `https://seu-projeto.up.railway.app/api/health`
- **Documentação**: `https://seu-projeto.up.railway.app/` (página inicial)

---

**Problema resolvido!** 🎉

A API Mock agora deve funcionar perfeitamente no Railway.
