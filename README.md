# Thoughtworks case

## 1. Arquitetura Final Proposta

### Visão Geral
Proposta de Arquitetura unificada baseada em um único webapp React SPA que se comunicará com os múltiplos backends existentes através de uma robusta camada BFF (Backend For Frontend).

### Componentes Principais

#### Frontend Unificado
- **Tecnologia**: React SPA (Single Page Application)
- **Estrutura**: Organização modular por domínios de negócio
- **Design System**: Sistema de design unificado para garantir consistência visual entre todos os fluxos
  - **Biblioteca de Componentes**: Conjunto compartilhado de componentes reutilizáveis

#### Camada BFF (Backend For Frontend)
- **Função**: Orquestração e agregação de dados de múltiplos backends
- **Implementação**: Node.js/Java ou tecnologia similar de alta performance de preferência com event loop para processos concorrentes
- **Recursos**:
  - Roteamento inteligente para os diferentes backends
  - Transformação e normalização de dados
  - Caching para otimização de performance
  - Circuit breaker para tolerância a falhas
  - Autenticação e autorização centralizadas

#### Backends Existentes
- Manutenção dos backends atuais em suas respectivas clouds (AWS, Google Cloud, Azure)
- Implementação gradual de interfaces padronizadas (contratos de API)
- Cada backend mantém sua responsabilidade por domínio (cadastro, reservas, pagamentos, busca...)

#### Infraestrutura e DevOps
- **CI/CD**: Pipeline unificado para build, teste e deployment
- **Observabilidade**: Centralização de logs, métricas e traces
- **Monitoramento**: Dashboards unificados para performance e disponibilidade
- **Analytics**: Consolidação de dados do Firebase Analytics
- **AutoScaling**: Ajuste automático de recursos de Cloud conforme a demanda

![Diagrama de Arquitetura](/thought_arch.png)

## 2. Plano de Implementação em Fases

### Fase 1: Setup inicial
- Estabelecer o design system e biblioteca de componentes
- Implementar a estrutura base do React SPA - seja reutilizando Viagens ou criando uma nova
- Desenvolver o primeiro protótipo da camada BFF - mesmo caso acima
- Implementar autenticação e autorização unificadas
- Manter os sistemas legados em operação paralelamente

### Fase 2: Primeira Integração
- Desenvolver o primeiro módulo completo no novo SPA (ex: Login/Cadastro ou uma página de detalhamento de reserva)
- Integrar o módulo com os backends através da camada BFF

### Fase 3: Migração Gradual
- Migrar módulo por módulo para o novo SPA seguindo prioridades de negócio
- Expandir a camada BFF para suportar todos os fluxos
- Iniciar teste A/B quando os fluxos de visualização, detalhamento e pagamento estiverem funcionais

### Fase 4: Consolidação e Otimização
- Migrar 100% do tráfego para o novo sistema
- Descomissionar os sites legados ou manter com redirects ao novo(por tempo determinado)
- Aumentar cobertura de testes automatizados

## 3. Formação de Times

### Estrutura Proposta
- **Core Team Frontend**: Responsável pelo design system, arquitetura e componentes core
- **Times de Produto**: Organizados por domínios de negócio/produto, time multidisciplinar - frontend, backend, QA, UX e product
- **Time de BFF e Integração**: Especializado na camada BFF e comunicação com backends de domínio, autenticação e segurança
- **Time de DevOps/Infraestrutura**: Suporte à infraestrutura unificada, criação de pipeline de CI/CD e conceito multicloud

### Modelo de Colaboração
- Adoção de Scrum para organização e colaboração intra e extra times
- Cerimônias conjuntas para alinhamento entre times em demendas cross
- Comunidades de tecnologia(Chapters) para compartilhamento de conhecimento (Frontend, Backend, DevOps)

## 4. Processos e Boas Práticas

### DevOps e CI/CD
- Criação de 3 ambientes -> Produção, Homologação e Development
- Pipeline unificado de CI/CD com stages bem definidos
- Integração contínua com testes automatizados
- Deployment automatizado para ambiente de development
- Aprovação para promoção Homologação -> Produção

### Qualidade e Testes
- Mínimo de 80% de cobertura de testes para código novo
- Testes de integração automatizados
- Testes de regressão antes de cada release
- Métricas de qualidade de código (SonarQube ou similar)

### Processo de Desenvolvimento
- Domain Driven Design e readequação de domínios quando necessário
- Gitflow ou adaptado às necessidades
- Refinamento contínuo de backlog, com reuniões semanais de discussão e aprofundamento
- Scrum com timebox de 2 semanas
- Feature flags para lançamentos graduais
- Code Review
- Pair programming

### Boas Práticas Técnicas
- Design system documentado e versionado - Figma ou similar
- Contratos de API bem definidos e testados - Swagger ou similar
- Design patterns consistentes - DDD, Clean architecture, clean code
- Logging e monitoramento padronizados - Datadog ou similar
- Estratégia de caching específica para cada funcionalidade

## 5. KPIs para Medir Desempenho dos Times

### Métricas de Desenvolvimento
- **Lead Time**: Tempo desde o início do desenvolvimento até o deploy em produção
- **Mean Time to Recovery (MTTR)**: Tempo médio para recuperação em caso de falhas
- **Technical Debt Ratio**: Monitoramento de dívida técnica

### Métricas de Qualidade
- **Test Coverage**: Percentual de código coberto por testes
- **Bug Escape Rate**: Bugs encontrados em produção vs. em QA
- **Code Quality Score**: Qualidade de código - SonarQube ou similar

### Métricas de Eficiência de Time(s)
- **Sprint Velocity**: Pontuação de entrega por sprint
- **Sprint Burndown**: Progresso dentro de cada sprint
- **Epic Burndown**: Progresso em iniciativas maiores
- **Cumulative Flow Diagram (CFD)** Monitora o fluxo de tarefas em diferentes estágios, ajudando a identificar gargalos e otimizar processos.

## 6. KPIs para Medir o Sucesso da Nova Solução

### Métricas de Negócio
- **Conversão**: Taxa de reservas concluídas vs iniciadas
- **Revenue per User**: Receita média por usuário
- **Churn Rate**: Taxa de abandono
- **Customer Acquisition Cost**: Custo de aquisição de novos clientes

### Métricas de Experiência do Usuário
- **Tempo de Carregamento**: Performance do frontend
- **Tempo de Resposta de API**: Latência das operações backend
- **Satisfação do Usuário**: Medida por NPS, CSAT ou ferramentas similares
- **Taxa de Abandono por Etapa**: Identificação de gargalos no funil de aquisição
- **Erro por Sessão**: Frequência de erros experimentados pelos usuários

### Métricas de Operação
- **Disponibilidade (Uptime)**: Percentual de tempo em que o sistema está disponível
- **Tempo de Resposta Médio**: Performance geral das APIs
- **Taxa de Erro de API**: Frequência de falhas nas APIs
- **Utilização de Recursos**: CPU, memória, rede
- **Custo de Infraestrutura**: Custo com recursos de cloud
