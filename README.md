# FinIA# FinIA — Gestão Financeira Inteligente

Aplicação web (PWA) para gestão financeira pessoal com IA integrada: controle de gastos, orçamento, acompanhamento de investimentos (ações, FIIs, cripto) e um assistente inteligente que analisa seus dados financeiros e gera insights personalizados.

![status](https://img.shields.io/badge/status-em%20desenvolvimento-yellow)
![license](https://img.shields.io/badge/license-MIT-blue)

<!-- 🖼️ Adicione aqui um GIF ou screenshot do dashboard assim que tiver a primeira versão funcional -->

## 🎯 Sobre o projeto

O FinIA nasceu da necessidade de unir, em um só lugar, o controle do dia a dia financeiro (gastos e orçamento) e o acompanhamento de investimentos — com uma camada de inteligência artificial que ajuda o usuário a entender seus próprios dados em vez de só exibir números.

Documentação completa do produto: veja [`docs/PRD.md`](./docs/PRD.md).

## ✨ Funcionalidades

- [ ] Cadastro e autenticação de usuários
- [ ] Lançamento e importação de transações (CSV/OFX)
- [ ] Categorização automática de gastos (IA)
- [ ] Orçamento mensal por categoria com alertas
- [ ] Dashboard com gráficos (gastos por categoria, evolução mensal)
- [ ] Carteira de investimentos (ações, FIIs, cripto, renda fixa)
- [ ] Cotações em tempo real via [Brapi.dev](https://brapi.dev)
- [ ] Assistente de IA conversacional com contexto dos dados do usuário
- [ ] Insights automáticos e alertas proativos
- [ ] Exportação de relatórios (PDF/Excel)
- [ ] PWA instalável (mobile e desktop)

## 🛠️ Stack técnica

| Camada | Tecnologia |
|---|---|
| Frontend | Next.js, TypeScript, Tailwind CSS, Recharts |
| Backend | Node.js (NestJS) *ou* Python (FastAPI) |
| Banco de dados | PostgreSQL + Redis (cache) |
| Autenticação | JWT / Clerk / Auth0 |
| IA | Claude API (Anthropic) |
| Dados de mercado | Brapi.dev (ações, FIIs, cripto, câmbio, macro) |
| Hospedagem | Vercel (frontend) + Railway/Render (backend) + Neon/Supabase (Postgres) |
| CI/CD | GitHub Actions |

## 🏗️ Arquitetura

```
┌─────────────┐      ┌──────────────┐      ┌────────────────┐
│  Frontend   │─────▶│   Backend    │─────▶│   PostgreSQL   │
│  (Next.js)  │◀─────│  (API REST)  │◀─────│    + Redis     │
└─────────────┘      └──────┬───────┘      └────────────────┘
                             │
                ┌────────────┼────────────┐
                ▼            ▼            ▼
          ┌──────────┐ ┌──────────┐ ┌───────────┐
          │ Brapi.dev│ │ Claude API│ │  OFX/CSV  │
          │ (cotações)│ │   (IA)   │ │ (importação)│
          └──────────┘ └──────────┘ └───────────┘
```

Detalhamento das decisões de arquitetura em [`docs/adr/`](./docs/adr).

## 🚀 Como rodar localmente

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/finia.git
cd finia

# Instale as dependências
npm install

# Configure as variáveis de ambiente
cp .env.example .env
# preencha .env com suas chaves (ver seção abaixo)

# Rode as migrations do banco
npm run migrate

# Inicie o projeto em modo desenvolvimento
npm run dev
```

Acesse `http://localhost:3000`.

## 🔑 Variáveis de ambiente

```env
DATABASE_URL=postgresql://user:password@localhost:5432/finia
REDIS_URL=redis://localhost:6379
JWT_SECRET=
BRAPI_TOKEN=
ANTHROPIC_API_KEY=
```

## 🗺️ Roadmap

- [x] Documentação inicial (PRD, arquitetura)
- [ ] Protótipo no Figma
- [ ] Modelagem do banco de dados
- [ ] MVP: controle de gastos
- [ ] Módulo de investimentos
- [ ] Assistente de IA
- [ ] Testes automatizados
- [ ] Deploy em produção

## 🤝 Contribuindo

Este é um projeto de portfólio pessoal, mas sugestões e issues são bem-vindas. Veja [`CONTRIBUTING.md`](./CONTRIBUTING.md) (a ser criado) para o fluxo de commits e branches.

## 📄 Licença

Distribuído sob a licença MIT. Veja [`LICENSE`](./LICENSE) para mais detalhes.

## 👤 Contato

**Caio Oliveira Silva Alencar** — [caioosalencar1523@gmai.com](mailto:caioosalencar1523@email.com)

Projeto: [https://github.com/caiooselncar1523-netizen/FinIA](https://github.com/seu-usuario/finia)