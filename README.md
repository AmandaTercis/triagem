# Assistente de Triagem — Núcleo SubPGMA

Wizard interativo que guia o triador pelo Fluxograma Macro do Núcleo de Triagem SubPGMA.

## Stack

- **Vite 5** + **React 18** + **TypeScript 5**
- **Tailwind CSS 3** (sem dependências de UI externas)
- Persistência via `localStorage`

## Como rodar

### 1. Instalar o Node.js

Baixe em: https://nodejs.org (versão LTS recomendada — 20.x ou 22.x)

### 2. Instalar dependências

```bash
npm install
```

### 3. Iniciar em desenvolvimento

```bash
npm run dev
```

Acesse em: **http://localhost:5173**

### 4. Build para produção

```bash
npm run build
```

Os arquivos ficam em `dist/`.

---

## Estrutura do projeto

```
src/
├── types/wizard.ts          # Tipos centrais (WizardState, StepId, etc.)
├── constants/               # Tema de cores + mapa de steps
├── mocks/                   # Hipóteses, procuradores, modelos de petição
├── hooks/                   # useWizard (estado + localStorage) + useClipboard
├── utils/                   # Validações por step + formatador de resumo
├── components/
│   ├── layout/              # WizardLayout + ProgressBar
│   ├── ui/                  # Button, Select, TextArea, CheckboxField, AlertBanner...
│   ├── shared/              # NavigationButtons, ValidationError
│   └── steps/               # Um componente por etapa do fluxo
└── pages/WizardPage.tsx     # Orquestra os steps via switch
```

## Regras-Âncora implementadas

| Regra | Onde |
|-------|------|
| Triador não encerra sozinho | Checkbox obrigatório em `StepEncerramentoObs` e `StepPeticaoDireta` |
| Redistribuição em 48h | AlertBanner vermelho fixo em `StepRedistribuicao` |
| Petição direta → Paola | Trava em `StepPeticaoDireta` |
| Ato processual → Procurador | Select obrigatório em `StepOficioAtoProcessual` |
