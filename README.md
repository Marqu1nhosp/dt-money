# DT Money

## Descrição

DT Money é uma aplicação web de controle financeiro pessoal que permite aos usuários registrar, visualizar e gerenciar suas transações de receitas e despesas. A aplicação fornece um painel resumido com informações de entradas, saídas e saldo total em tempo real.

## Problema que o Projeto Resolve

A dificuldade em acompanhar receitas e despesas no dia a dia é uma das principais causas de desorganização financeira pessoal. DT Money resolve esse problema oferecendo:

- Uma plataforma simples e intuitiva para registrar transações financeiras
- Visualização clara dos gastos por categoria
- Cálculo automático do saldo final
- Busca e filtragem de transações
- Interface responsiva e acessível

## Demonstração

A aplicação apresenta uma interface limpa com:

- **Header**: Logo e botão para nova transação
- **Summary Cards**: Exibição de receitas totais, despesas totais e saldo
- **Transactions Table**: Lista de todas as transações com descrição, valor, categoria e data
- **Search Form**: Busca por transações específicas

## Tecnologias Utilizadas

### Frontend

- **React** 18.2.0 - Biblioteca JavaScript para construção de UI
- **TypeScript** 4.9.3 - Linguagem com tipagem estática
- **Vite** 4.2.0 - Bundler rápido e moderno
- **Styled Components** 5.3.9 - CSS-in-JS para estilos scoped
- **React Hook Form** 7.43.9 - Gerenciamento eficiente de formulários
- **Zod** 3.21.4 - Validação de esquema TypeScript-first
- **Axios** 1.3.4 - Cliente HTTP para requisições
- **Radix UI** - Componentes acessíveis e sem estilo
  - react-dialog: Modais acessíveis
  - react-radio-group: Grupos de rádio acessíveis
- **Phosphor React** 1.4.1 - Ícones customizáveis
- **use-context-selector** 1.4.1 - Seletor otimizado para Context API

### Backend Mock

- **JSON Server** 0.17.3 - Servidor REST simulado com dados em JSON

### Desenvolvimento

- **ESLint** 8.37.0 - Linting de código
- **@rocketseat/eslint-config** 1.2.0 - Configuração ESLint padronizada

## Arquitetura do Projeto

### Padrão Arquitetural: Component-Based com Context API

A aplicação segue uma arquitetura modular baseada em componentes, utilizando Context API para gerenciamento de estado global. O padrão evita prop drilling e oferece otimizações de performance através do `use-context-selector`.

```
┌─────────────────────────────────────────────┐
│         Componentes Apresentacionais          │
│  (Header, Summary, NewTransactionModal)      │
└──────────────────┬──────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────┐
│          Custom Hooks (useSummary)           │
│        (Lógica compartilhada e reutilização) │
└──────────────────┬──────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────┐
│     Context API + use-context-selector       │
│     (TransactionsContext - Estado Global)    │
└──────────────────┬──────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────┐
│         Camada de Integração                 │
│  (axios - Comunicação com JSON Server)       │
└─────────────────────────────────────────────┘
```

### Divisão de Responsabilidades

**Components (`/src/components`)**

- Componentes reutilizáveis e apresentacionais
- Header: Exibe logo e botão de nova transação
- Summary: Cartas com resumo financeiro (entradas, saídas, total)
- NewTransactionModal: Formulário para registro de novas transações

**Pages (`/src/pages`)**

- Telas/páginas da aplicação
- Transactions: Página principal com tabela de transações e busca

**Contexts (`/src/contexts`)**

- TransactionsContext: Gerencia estado global de transações
- Funções: fetchTransactions, createTransaction
- Fornece tipagem TypeScript para o contexto

**Hooks (`/src/hooks`)**

- useSummary: Calcula resumo financeiro (receitas, despesas, total)
- Utiliza useMemo para otimização de cálculos

**Utils (`/src/utils`)**

- formatter.ts: Formatadores reutilizáveis
  - dateFormatter: Formata datas em pt-BR
  - priceFormatter: Formata valores em BRL

**Lib (`/src/lib`)**

- axios.ts: Instância axios configurada com baseURL

**Styles (`/src/styles`)**

- global.ts: Estilos globais da aplicação
- themes/default.ts: Paleta de cores padrão

## Estrutura de Pastas Explicada

```
dt-money/
├── public/                     # Arquivos estáticos públicos
├── src/
│   ├── @types/
│   │   └── styles.d.ts        # Tipos para styled-components
│   ├── assets/                # Imagens, ícones e recursos estáticos
│   ├── components/            # Componentes reutilizáveis
│   │   ├── Header/            # Cabeçalho da aplicação
│   │   ├── NewTransactionModal/ # Modal para nova transação
│   │   └── Summary/           # Cards de resumo financeiro
│   ├── contexts/              # Context API
│   │   └── TransactionsContext.tsx # Contexto global de transações
│   ├── hooks/                 # Custom hooks
│   │   └── useSummary.ts      # Hook para cálculo de resumo
│   ├── lib/                   # Bibliotecas/instâncias configuradas
│   │   └── axios.ts           # Cliente axios configurado
│   ├── pages/                 # Páginas/telas da aplicação
│   │   └── Transactions/
│   │       ├── index.tsx      # Página principal
│   │       ├── styles.ts      # Estilos da página
│   │       └── components/
│   │           └── SearchForm/ # Formulário de busca
│   ├── styles/                # Estilos globais e temas
│   │   ├── global.ts          # Estilos globais
│   │   └── themes/
│   │       └── default.ts     # Tema padrão (cores)
│   ├── utils/                 # Funções utilitárias
│   │   └── formatter.ts       # Formatadores de dados
│   ├── App.tsx                # Componente raiz
│   ├── main.tsx               # Ponto de entrada
│   └── vite-env.d.ts          # Tipos do Vite
├── index.html                 # Arquivo HTML principal
├── package.json               # Dependências e scripts
├── server.json                # Dados simulados para JSON Server
├── tsconfig.json              # Configuração TypeScript
├── vite.config.ts             # Configuração Vite
└── README.md                  # Esta documentação
```

## Como Rodar o Projeto Localmente

### Pré-requisitos

Certifique-se de que você possui os seguintes softwares instalados:

- **Node.js** (versão 16.x ou superior)
- **npm** ou **yarn** (gerenciador de pacotes)
- **Git** (para clonar o repositório)

### Instalação

1. Clone o repositório:

```bash
git clone https://github.com/seu-usuario/dt-money.git
cd dt-money
```

2. Instale as dependências:

```bash
npm install
```

### Rodando a Aplicação

A aplicação requer dois terminais para rodar simultaneamente:

**Terminal 1 - Servidor de desenvolvimento (Frontend):**

```bash
npm run dev
```

A aplicação estará disponível em: `http://localhost:5173`

**Terminal 2 - Servidor mockado (Backend):**

```bash
npm run dev:server
```

O servidor REST estará disponível em: `http://localhost:3333`

Ambos os servidores devem estar rodando simultaneamente para a aplicação funcionar corretamente.

## Scripts Disponíveis

```bash
# Inicia servidor de desenvolvimento (Vite)
npm run dev

# Inicia servidor REST mockado (JSON Server)
npm run dev:server

# Executa linting de código
npm run lint

# Corrige automaticamente erros de linting
npm run lint:fix

# Build de produção (gera arquivos otimizados)
npm run build

# Visualiza build de produção localmente
npm run preview
```

## Exemplos de Uso da Aplicação

### 1. Visualizar Transações Existentes

Ao abrir a aplicação, você verá automaticamente todas as transações carregadas do servidor. O painel Summary exibe:

- **Entradas**: Total de todas as receitas
- **Saídas**: Total de todas as despesas
- **Total**: Saldo final (receitas - despesas)

### 2. Registrar uma Nova Transação

1. Clique no botão "Nova transação" no header
2. Preencha os campos:
   - **Descrição**: Nome da transação (ex: "Salário", "Padaria")
   - **Preço**: Valor em números (ex: 1500, 25.50)
   - **Categoria**: Tipo de categoria (ex: "Venda", "Alimentação")
   - **Tipo**: Selecione "Receita" (entrada) ou "Despesa" (saída)
3. Clique em "Registrar"
4. A transação será adicionada automaticamente à lista

### 3. Buscar Transações

1. Utilize o formulário de busca acima da tabela
2. Digite parte da descrição que procura
3. Clique em "Buscar" ou pressione Enter
4. A tabela filtrará para mostrar apenas transações correspondentes

### 4. Visualizar Detalhes da Transação

A tabela exibe as seguintes informações:

- **Descrição**: Nome da transação
- **Valor**: Valor com símbolo de moeda, negativo para despesas
- **Categoria**: Tipo de categoria
- **Data**: Data formatada em pt-BR

## Fluxo de Dados da Aplicação

```
┌─────────────────────────────────────────────┐
│  Usuário Interage com a Interface (UI)     │
└────────────────┬────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────────┐
│  Componentes Apresentacionais Disparam      │
│  Ações (ex: Nova Transação, Busca)          │
└────────────────┬────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────────┐
│  Custom Hooks / Context Processam           │
│  a Lógica (validação, cálculo)              │
└────────────────┬────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────────┐
│  TransactionsContext Gerencia o Estado      │
│  e Chamadas à API (Axios)                   │
└────────────────┬────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────────┐
│  JSON Server Retorna Dados / Confirma       │
│  Operação (CREATE, READ)                    │
└────────────────┬────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────────┐
│  Estado é Atualizado no Context             │
│  Componentes Re-renderizam                  │
└─────────────────────────────────────────────┘
```

## Boas Práticas Utilizadas no Projeto

### 1. Separação de Responsabilidades

- Componentes apresentacionais isolados da lógica
- Contextos dedicados ao estado global
- Hooks customizados para lógica reutilizável
- Utilitários para funções genéricas

### 2. Tipagem TypeScript Forte

- Interfaces bem definidas para estruturas de dados
- Props tipadas em componentes
- Tipos inferidos do Zod para formulários

### 3. Gerenciamento de Estado Otimizado

- Context API com `use-context-selector` para evitar re-renders desnecessários
- `useCallback` no contexto para memoizar funções
- `useMemo` no hook `useSummary` para cálculos otimizados

### 4. Validação Robusta

- Zod para validação de esquema em tempo de execução
- Validação em formulários com React Hook Form
- Tipos inferidos automaticamente do schema Zod

### 5. Acessibilidade

- Componentes Radix UI já acessíveis por padrão
- Dialogo modal com controle de foco
- Semântica correta de HTML

### 6. Padrão de Formulários

- React Hook Form para gerenciamento eficiente
- Controller do React Hook Form para componentes customizados
- Integração com Zod para validação

### 7. Formatação Internacionalizada

- Intl API do JavaScript para localização
- Datas e moedas formatadas em pt-BR (português brasileiro)
- Fácil adaptação para outras localidades

### 8. Organização de Código

- Estrutura de pastas clara e escalável
- Nomes descritivos de arquivos e variáveis
- Comentários explicativos em pontos críticos

### 9. Performance

- Lazy loading potencial (pronto para implementação)
- Otimizações com useMemo e useCallback
- CSS-in-JS scoped com Styled Components

### 10. Estilo de Código

- Config ESLint padronizada (@rocketseat)
- Consistência de formatação
- Scripts para lint e fix automático

## Endpoints da API REST

A aplicação comunica com JSON Server nos seguintes endpoints:

### GET /transactions

Recupera todas as transações com suporte a filtros.

**Parâmetros Query:**

```
_sort=createdAt    # Ordena por data de criação
_order=desc        # Ordem decrescente (mais recentes primeiro)
q=<query>          # Busca por descrição (search query)
```

**Exemplo de Requisição:**

```bash
GET http://localhost:3333/transactions?_sort=createdAt&_order=desc&q=salário
```

**Resposta:**

```json
[
  {
    "id": 1,
    "description": "Desenvolvimento",
    "type": "income",
    "category": "venda",
    "price": 14000,
    "createdAt": "2023-03-29T22:54:10.953Z"
  }
]
```

### POST /transactions

Cria uma nova transação.

**Body (JSON):**

```json
{
  "description": "Novo projeto",
  "price": 5000,
  "category": "Venda",
  "type": "income",
  "createdAt": "2023-04-01T21:29:07.669Z"
}
```

**Resposta:**

```json
{
  "id": 7,
  "description": "Novo projeto",
  "type": "income",
  "category": "Venda",
  "price": 5000,
  "createdAt": "2023-04-01T21:29:07.669Z"
}
```

## Tipos de Dados

### Transaction Interface

```typescript
interface Transaction {
  id: number; // Identificador único
  description: string; // Descrição da transação
  type: "income" | "outcome"; // Tipo: receita ou despesa
  price: number; // Valor da transação
  category: string; // Categoria (ex: Alimentação, Venda)
  createdAt: string; // Data de criação (ISO 8601)
}
```

### CreateTransactionInput Interface

```typescript
interface CreateTransactionInput {
  description: string; // Descrição da transação
  price: number; // Valor da transação
  category: string; // Categoria da transação
  type: "income" | "outcome"; // Tipo de transação
}
```

### Summary Interface

```typescript
interface Summary {
  income: number; // Total de receitas
  outcome: number; // Total de despesas
  total: number; // Saldo final (income - outcome)
}
```

## Conclusão

DT Money é uma aplicação bem estruturada que demonstra excelentes práticas de desenvolvimento React moderno. A arquitetura baseada em componentes, aliada ao uso inteligente de Context API e hooks customizados, oferece uma base sólida para futuras expansões e melhorias.
