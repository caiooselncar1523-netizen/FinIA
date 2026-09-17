# PRD — Product Requirements Document
## FinIA — Gestão Financeira Inteligente

**Versão:** 0.1 (rascunho)
**Autor:** [Caio Oliveira Silva Alencar]
**Última atualização:** 2026-09-17
**Status:** Em planejamento

---

## 1. Visão geral

O FinIA é uma aplicação web (PWA) de gestão financeira pessoal que combina três pilares em uma única plataforma:

1. **Controle de gastos** — lançamento, categorização e orçamento.
2. **Acompanhamento de investimentos** — carteira, cotações em tempo real, evolução patrimonial.
3. **Assistente de IA** — análise dos dados do próprio usuário e geração de insights.

## 2. Problema

Pessoas físicas geralmente usam ferramentas separadas (planilhas para gastos, app do banco para extrato, home broker para investimentos) e não têm uma visão unificada da própria saúde financeira. Ferramentas existentes no mercado ou são pagas, ou não têm inteligência real (só mostram números, sem interpretar).

## 3. Objetivos do produto

- Unificar controle de gastos e acompanhamento de investimentos em uma única interface.
- Reduzir o esforço manual de categorização e análise usando IA.
- Gerar insights acionáveis, não apenas dashboards estáticos.

### 3.1 Objetivos não-funcionais (para este projeto como portfólio)

- Demonstrar domínio de arquitetura full-stack, modelagem de dados e integração com APIs externas.
- Ter documentação e testes que evidenciem maturidade profissional.
- Ser um projeto "vivo" — evoluível em fases, cada uma com entregas visíveis.

## 4. Público-alvo / Personas

**Persona 1 — "Rafael, 28 anos, CLT"**
Ganha bem, mas não sabe pra onde vai o dinheiro. Quer entender seus gastos e começar a investir com mais consciência.

**Persona 2 — "Marina, 34 anos, investidora iniciante"**
Já investe um pouco (ações e Tesouro Direto), mas não tem uma visão consolidada da carteira e quer acompanhar rentabilidade num só lugar.

## 5. Escopo do MVP

### Dentro do escopo (MVP)
- Cadastro/login de usuário
- Lançamento manual de transações (receita/despesa)
- Categorização de transações (manual + sugestão automática simples)
- Dashboard com gráficos de gastos por categoria e por período
- Orçamento mensal por categoria com indicador de progresso
- Cadastro manual de ativos (ticker, quantidade, preço médio)
- Cotação em tempo real via Brapi.dev
- Evolução patrimonial simples (gráfico de valor total da carteira ao longo do tempo)
- Chat com assistente de IA com acesso aos dados do usuário

### Fora do escopo (MVP) — fica para fases seguintes
- Importação automática via Open Finance / conexão direta com bancos
- Recomendação personalizada de compra/venda de ativos (implica regulação CVM — ver seção de riscos)
- App nativo (iOS/Android) — fica PWA por enquanto
- Múltiplas moedas / usuários fora do Brasil
- Compartilhamento de conta entre múltiplos usuários (conta conjunta, família)

### 5.1 Comportamento e limites do assistente de IA

Decisão de produto (confirmada em 2026-09-17): o assistente deve ter um nível de "opinião" intermediário — nem passivo demais, nem arriscado do ponto de vista regulatório.

**O assistente PODE:**
- Analisar padrões de gastos e apontar tendências ("seus gastos com delivery subiram 40% este mês")
- Sugerir ajustes de orçamento e hábitos financeiros ("considerando seu gasto médio, talvez valha reduzir a categoria X")
- Explicar dados da carteira de investimentos (rentabilidade, concentração, evolução)
- Responder perguntas educativas sobre finanças e investimentos de forma genérica

**O assistente NÃO PODE:**
- Recomendar compra ou venda de um ativo específico ("compre mais PETR4", "venda seus FIIs")
- Fazer projeções de rentabilidade futura de ativos específicos como se fosse garantia
- Dar qualquer conselho que se enquadre como consultoria de investimento personalizada (regulada pela CVM)

Essa fronteira deve estar refletida tanto no prompt de sistema do assistente quanto em um aviso visível na interface do chat ("este assistente não fornece recomendações de investimento").

## 6. Requisitos funcionais

| ID | Requisito | Prioridade |
|---|---|---|
| RF01 | Usuário deve poder se cadastrar e autenticar | Alta |
| RF02 | Usuário deve poder lançar transações manualmente | Alta |
| RF03 | Sistema deve sugerir categoria automaticamente com base na descrição | Média |
| RF04 | Usuário deve poder definir orçamento mensal por categoria | Alta |
| RF05 | Sistema deve alertar quando orçamento de uma categoria for ultrapassado | Média |
| RF06 | Usuário deve poder cadastrar ativos da carteira | Alta |
| RF07 | Sistema deve buscar cotações atualizadas via API externa | Alta |
| RF08 | Usuário deve poder conversar com assistente de IA sobre seus dados (gastos e carteira) | Alta |
| RF09 | Sistema deve gerar ao menos 1 insight automático por semana (padrões de gasto, sugestões de orçamento) | Baixa |
| RF10 | Assistente deve recusar/redirecionar pedidos de recomendação de compra/venda de ativos específicos, mantendo o foco em análise e educação | Alta |
| RF11 | Usuário deve poder exportar relatório em PDF | Baixa |

## 7. Requisitos não-funcionais

- **Segurança:** dados sensíveis (senha, tokens) criptografados; conformidade com LGPD.
- **Performance:** carregamento do dashboard em menos de 2s com dados em cache.
- **Disponibilidade:** cache de cotações (Redis) para não depender 100% da API externa em tempo real.
- **Responsividade:** interface funcional em mobile e desktop (mobile-first).

## 8. Métricas de sucesso (mesmo sendo projeto de portfólio)

- Cobertura de testes automatizados > 70% no backend.
- Tempo de resposta médio da API < 300ms.
- Pipeline de CI/CD funcionando (lint, testes, build automatizados a cada PR).

## 9. Riscos e considerações

- **Regulatório:** o assistente de IA não deve emitir recomendações de compra/venda de ativos específicos — isso configura consultoria de investimentos, regulada pela CVM. O foco deve ser em informação, organização e análise, não em recomendação personalizada de investimento.
- **Dependência de API externa:** o plano gratuito da Brapi.dev tem limite de requisições/mês — necessário implementar cache (Redis) para não estourar o limite.
- **Dados sensíveis:** por lidar com dados financeiros, atenção redobrada a criptografia e boas práticas de segurança (mesmo em projeto de portfólio, isso é o que um recrutador técnico vai observar).

## 10. Fases de desenvolvimento

| Fase | Entregável |
|---|---|
| 1 | Documentação + Figma (protótipo navegável) |
| 2 | Modelagem de banco de dados |
| 3 | MVP — controle de gastos (backend + frontend) |
| 4 | Módulo de investimentos |
| 5 | Assistente de IA |
| 6 | Testes automatizados |
| 7 | Deploy + apresentação em portfólio |

## 11. Referências

- API de dados de mercado: [Brapi.dev](https://brapi.dev/docs)
- Diagramas de arquitetura: `docs/adr/`
- Protótipo Figma: ...