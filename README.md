# 📊 Agente de Carteira de Investimentos

> Análise inteligente da sua carteira com Python e IA — relatórios em linguagem natural, métricas quantitativas e sugestões de rebalanceamento.

---
 
## Sobre o projeto

O **Agente de Carteira** é uma ferramenta de linha de comando que conecta dados financeiros em tempo real com modelos de linguagem (LLMs) para transformar números em insights acionáveis. Você informa sua carteira, e o agente calcula métricas como Sharpe Ratio, volatilidade e correlação entre ativos — depois pede à IA para explicar tudo em português claro.

---

## Funcionalidades

- **Cotações em tempo real** via [brapi.dev](https://brapi.dev) (B3) e yfinance (internacionais)
- **Métricas quantitativas**: retorno, volatilidade, Sharpe Ratio, correlação, drawdown
- **Comparação com benchmarks**: IBOV, CDI, S&P500
- **Alerta de concentração** por setor
- **Relatório narrativo em PT-BR** gerado por LLM
- **Sugestão de rebalanceamento** com base nas métricas
- **Q&A conversacional** sobre sua carteira
- **Exportação em PDF** e dashboard opcional com Streamlit

---

## Stack

| Camada | Tecnologia |
|---|---|
| Linguagem | Python 3.11+ |
| Dados financeiros | brapi.dev, yfinance |
| Análise de dados | Pandas, NumPy |
| IA / LLM | Anthropic Claude API |
| Interface CLI | Rich |
| Visualização | Matplotlib, Plotly |
| Relatório PDF | ReportLab |
| Dashboard (opcional) | Streamlit |

---

## Estrutura do projeto

```
agente-carteira/
├── src/
│   ├── carteira/
│   │   ├── __init__.py
│   │   ├── models.py          # Entidades: Carteira, Ativo, Operação
│   │   └── portfolio.py       # Lógica de cálculo e métricas
│   ├── data/
│   │   ├── brapi.py           # Integração brapi.dev (B3)
│   │   └── yfinance.py        # Integração Yahoo Finance
│   ├── analise/
│   │   ├── metricas.py        # Sharpe, volatilidade, correlação
│   │   └── benchmarks.py      # Comparação IBOV, CDI, S&P500
│   ├── ia/
│   │   ├── agente.py          # Orquestração das chamadas ao LLM
│   │   ├── relatorio.py       # Geração de relatório narrativo
│   │   └── rebalanceamento.py # Sugestões de ajuste de carteira
│   └── interface/
│       ├── cli.py             # Menu interativo com Rich
│       └── pdf.py             # Exportação de relatório
├── data/
│   └── carteira.json          # Arquivo de entrada da carteira
├── tests/
├── .env.example
├── pyproject.toml
└── README.md
```

---

## Instalação

### Pré-requisitos

- Python 3.11+
- Conta na [Anthropic](https://console.anthropic.com) para obter a API key
- (Opcional) Token da [brapi.dev](https://brapi.dev) para cotações B3

### Passo a passo

```bash
# 1. Clone o repositório
git clone https://github.com/seu-usuario/agente-carteira.git
cd agente-carteira

# 2. Crie e ative o ambiente virtual
python -m venv .venv
source .venv/bin/activate  # Linux/macOS
.venv\Scripts\activate     # Windows

# 3. Instale as dependências
pip install -e .

# 4. Configure as variáveis de ambiente
cp .env.example .env
# Edite o .env com suas chaves
```

### Variáveis de ambiente

```env
ANTHROPIC_API_KEY=sk-ant-...
BRAPI_TOKEN=seu_token_aqui   # opcional, aumenta o rate limit
```

---

## Como usar

### 1. Defina sua carteira

Edite o arquivo `data/carteira.json`:

```json
{
  "ativos": [
    { "ticker": "PETR4", "quantidade": 100, "preco_medio": 35.50 },
    { "ticker": "MXRF11", "quantidade": 200, "preco_medio": 10.20 },
    { "ticker": "BTC-USD", "quantidade": 0.05, "preco_medio": 280000 }
  ]
}
```

### 2. Rode o agente

```bash
# Análise completa com relatório da IA
python -m agente_carteira analyze

# Só as métricas (sem IA)
python -m agente_carteira metrics

# Chat com o agente sobre sua carteira
python -m agente_carteira chat

# Exportar relatório em PDF
python -m agente_carteira report --output relatorio.pdf
```

### 3. Exemplo de saída

```
╭─────────────────────────────────────────╮
│         Análise da Carteira             │
╰─────────────────────────────────────────╯

 Ativo     Peso    Retorno    Sharpe   Volatilidade
 PETR4     45%      +12.3%     0.87      18.2%
 MXRF11    35%       +8.1%     1.12      11.4%
 BTC-USD   20%      +31.5%     0.63      54.7%

 vs IBOV:  +5.2%  ✓ acima do benchmark

📝 Análise gerada por IA:
"Sua carteira apresenta retorno sólido, mas a alocação
de 45% em PETR4 gera concentração no setor de energia.
Considere reduzir para ~30% e diversificar em..."
```

---

## Roadmap

### Sprint 1 — Fundação
- [x] Estrutura do projeto e modelos de dados
- [ ] Integração brapi.dev e yfinance
- [ ] Cálculo de retorno e marcação a mercado

### Sprint 2 — Métricas Quantitativas
- [ ] Sharpe Ratio, volatilidade, correlação
- [ ] Comparação com benchmarks
- [ ] Alerta de concentração por setor

### Sprint 3 — Inteligência Artificial
- [ ] Relatório narrativo com LLM
- [ ] Sugestão de rebalanceamento
- [ ] Chat Q&A sobre a carteira

### Sprint 4 — Interface & Entrega
- [ ] CLI com Rich
- [ ] Exportação em PDF
- [ ] Dashboard Streamlit (opcional)
- [ ] Notificações via Telegram

---

## Contribuindo

Contribuições são bem-vindas! Siga o fluxo:

1. Fork o repositório
2. Crie uma branch: `git checkout -b feature/nome-da-feature`
3. Commit suas mudanças: `git commit -m 'feat: adiciona análise de dividendos'`
4. Push para a branch: `git push origin feature/nome-da-feature`
5. Abra um Pull Request

---

## Licença

Distribuído sob a licença MIT. Veja `LICENSE` para mais informações.

---

## Integrantes do Projeto

Alexandre Silva Alves - RM567415
Julia Marcela de Faria Bonifacio - RM566673
Mariana Pergentino Fonseca - RM568252
Pedro Iavarone Custódio - RM567638

---
> Feito com Python + IA para investidores brasileiros 🇧🇷
