# 🚀 RetechLog API Mock

**Servidor mock inteligente para simulação de APIs do ecossistema RetechLog** - desenvolvido com Next.js 14 e TypeScript para fornecer dados realistas durante desenvolvimento e testes.

## 📋 Sobre o Projeto

O **RetechLog API Mock** é um servidor de simulação que centraliza todos os endpoints mockados necessários para o desenvolvimento e teste das aplicações do ecossistema RetechLog. Ele fornece respostas realistas e consistentes para autenticação, produtos, blog, calendário, kanban, chat, mail e outros módulos, permitindo desenvolvimento frontend independente da API real.

### 🎯 Objetivos Principais

- **Desenvolvimento Independente**: Permite que equipes frontend trabalhem sem dependência da API real
- **Testes Automatizados**: Fornece dados consistentes para testes E2E e de integração
- **Prototipagem Rápida**: Facilita validação de UX/UI com dados realistas
- **Ambiente Isolado**: Reduz dependências externas durante desenvolvimento

## 🛠 Stack Tecnológica

### Core
- **Next.js 14** - Framework React com App Router
- **TypeScript 5.8** - Tipagem estática
- **React 18** - Interface de usuário
- **Node.js 20+** - Runtime JavaScript

### UI & Styling
- **Material-UI (MUI) 6** - Componentes de interface
- **Emotion** - CSS-in-JS styling
- **Day.js** - Manipulação de datas

### Desenvolvimento
- **ESLint 9** - Linting de código
- **Prettier 3** - Formatação de código
- **Yarn 1.22** - Gerenciador de pacotes

### Infraestrutura
- **Railway** - Deploy e hospedagem
- **Docker** - Containerização
- **Next.js Standalone** - Build otimizado

## 🚀 Início Rápido

### Pré-requisitos
- Node.js >= 20
- Yarn ou npm
- Conta no Railway (para deploy)

### Instalação Local

```bash
# Clonar repositório
git clone <repository-url>
cd retechlog-api-mock

# Instalar dependências
yarn install
# ou
npm install

# Configurar variáveis de ambiente
cp env.example .env.local

# Executar em modo desenvolvimento
yarn dev
# ou
npm run dev
```

**Servidor disponível em:** [http://localhost:7272](http://localhost:7272)

### Deploy no Railway

```bash
# 1. Conectar repositório no Railway Dashboard
# 2. Configurar variáveis de ambiente
# 3. Deploy automático via GitHub

# Veja RAILWAY_DEPLOY.md para instruções detalhadas
```

## 📚 API Endpoints

### 🔐 Autenticação
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| `GET` | `/api/auth/me` | Obter informações do usuário logado |
| `POST` | `/api/auth/sign-in` | Login de usuário |
| `POST` | `/api/auth/sign-up` | Registro de usuário |

### 📦 Produtos
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| `GET` | `/api/product/list` | Listar todos os produtos |
| `GET` | `/api/product/details?productId={id}` | Detalhes do produto |
| `GET` | `/api/product/search?query={query}` | Buscar produtos |

### 📝 Blog
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| `GET` | `/api/post/list` | Listar posts |
| `GET` | `/api/post/details?title={title}` | Detalhes do post |
| `GET` | `/api/post/latest` | Posts mais recentes |
| `GET` | `/api/post/search?query={query}` | Buscar posts |

### 📅 Calendário
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| `GET` | `/api/calendar` | Listar eventos |
| `POST` | `/api/calendar` | Criar evento |
| `PUT` | `/api/calendar` | Atualizar evento |
| `PATCH` | `/api/calendar` | Excluir evento |

### 📋 Kanban
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| `GET` | `/api/kanban` | Obter board |
| `POST` | `/api/kanban?endpoint=create-column` | Criar coluna |
| `POST` | `/api/kanban?endpoint=update-column` | Atualizar coluna |
| `POST` | `/api/kanban?endpoint=move-column` | Mover coluna |
| `POST` | `/api/kanban?endpoint=delete-column` | Excluir coluna |
| `POST` | `/api/kanban?endpoint=create-task` | Criar tarefa |
| `POST` | `/api/kanban?endpoint=update-task` | Atualizar tarefa |
| `POST` | `/api/kanban?endpoint=move-task` | Mover tarefa |
| `POST` | `/api/kanban?endpoint=delete-task` | Excluir tarefa |

### 💬 Chat
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| `GET` | `/api/chat?endpoint=contacts` | Listar contatos |
| `GET` | `/api/chat?endpoint=conversations` | Listar conversas |
| `GET` | `/api/chat?conversationId={id}&endpoint=conversation` | Detalhes da conversa |
| `GET` | `/api/chat?conversationId={id}&endpoint=mark-as-seen` | Marcar como lida |
| `POST` | `/api/chat` | Criar conversa |
| `PUT` | `/api/chat` | Atualizar conversa |

### 📧 Mail
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| `GET` | `/api/mail/labels` | Listar labels |
| `GET` | `/api/mail/list?labelId={id}` | Listar emails por label |
| `GET` | `/api/mail/details?mailId={id}` | Detalhes do email |

### 🧭 Navegação
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| `GET` | `/api/navbar` | Obter itens de navegação |

### 📄 Paginação
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| `GET` | `/api/pagination?page={page}&perPage={perPage}` | Dados paginados |

## ⚙️ Configuração

### Variáveis de Ambiente

Copie `env.example` para `.env.local` e configure:

```bash
# Servidor
NODE_ENV=development
PORT=7272
HOST=0.0.0.0

# APIs
DEV_API=http://localhost:7272
PRODUCTION_API=https://api-mock.retechlog.com

# CORS
CORS_ALLOWED_ORIGINS=http://localhost:8082,http://localhost:3000
CORS_METHODS=GET,POST,PUT,PATCH,DELETE,OPTIONS

# JWT (Mock)
JWT_SECRET=your-super-secret-jwt-key
JWT_EXPIRES_IN=7d

# Cache (Opcional)
REDIS_URL=redis://localhost:6379
CACHE_TTL=3600

# Mock Data
MOCK_DELAY_MIN=100
MOCK_DELAY_MAX=500
MOCK_ERROR_RATE=0.05
```

### Railway Deploy

O deploy no Railway é simples e automático:

- **GitHub Integration**: Deploy automático a cada push
- **Environment Variables**: Configuração via dashboard
- **SSL Automático**: HTTPS incluso
- **Logs em Tempo Real**: Dashboard integrado

## 🔧 Scripts Disponíveis

```bash
# Desenvolvimento
yarn dev              # Servidor de desenvolvimento
yarn build            # Build de produção
yarn start            # Servidor de produção
yarn clean            # Limpar build e dependências

# Qualidade de código
yarn lint             # Verificar linting
yarn lint:fix         # Corrigir problemas de lint
yarn fm:check         # Verificar formatação
yarn fm:fix           # Corrigir formatação
yarn fix:all          # Corrigir tudo

# Utilitários
yarn re:dev           # Reinstalar e executar dev
yarn re:build         # Reinstalar e build
yarn tsc:watch        # TypeScript em modo watch
```

## 🚂 Deploy no Railway

### Deploy Simples
```bash
# 1. Conectar repositório no Railway Dashboard
# 2. Configurar variáveis de ambiente
# 3. Deploy automático via GitHub

# Variáveis importantes no Railway:
NODE_ENV=production
JWT_SECRET=sua-chave-jwt-secreta
CORS_ALLOWED_ORIGINS=http://localhost:8082,http://localhost:3000
```

### URLs após Deploy
- **Railway URL**: `https://seu-projeto.up.railway.app`
- **Health Check**: `https://seu-projeto.up.railway.app/api/health`

## 📊 Monitoramento

### Health Check
```bash
curl https://seu-projeto.up.railway.app/api/health
```

### Logs
- **Railway Dashboard**: Logs em tempo real
- **CLI**: `railway logs` (se usando Railway CLI)

## 🚀 Deploy

### Railway (Recomendado)
```bash
# Deploy automático via GitHub
# 1. Conectar repositório no Railway Dashboard
# 2. Configurar variáveis de ambiente
# 3. Deploy automático

# Veja RAILWAY_DEPLOY.md para instruções detalhadas
```

### Vercel (Alternativo)
```bash
# Deploy automático via Git
vercel --prod
```

### Cloudflare Pages (Alternativo)
```bash
# Build command
npx @cloudflare/next-on-pages@1

# Build output directory
.vercel/output/static
```

## 🤝 Contribuição

1. Fork o projeto
2. Crie uma branch (`git checkout -b feature/nova-feature`)
3. Commit suas mudanças (`git commit -am 'Adiciona nova feature'`)
4. Push para a branch (`git push origin feature/nova-feature`)
5. Abra um Pull Request

## 📝 Licença

Este projeto está sob a licença MIT. Veja o arquivo `LICENSE` para detalhes.

## 📞 Suporte

- **Documentação**: [Minimal Docs](https://docs.minimals.cc/quick-start)
- **Issues**: [GitHub Issues](https://github.com/your-repo/issues)
- **Email**: suporte@retechlog.com

---

**Desenvolvido com ❤️ pela equipe RetechLog**