# 🔧 Sistema de Ordens de Serviço — OS Manager

Sistema completo de gerenciamento de Ordens de Serviço para ambientes industriais.

## 📦 Estrutura do Projeto

```
os-system/
├── app.py              # Backend Flask + SQLite
├── os_system.db        # Banco de dados (gerado automaticamente)
├── requirements.txt    # Dependências Python
├── start.sh            # Script de inicialização
└── templates/
    └── index.html      # Frontend completo (HTML/CSS/JS)
```

## ⚙️ Instalação

```bash
# 1. Instalar dependências
pip install -r requirements.txt

# 2. Iniciar o servidor
python app.py
# ou
bash start.sh

# 3. Acessar no navegador
http://localhost:5050
```

## 🚀 Funcionalidades

### Ordens de Serviço
- ✅ Cadastro com título, descrição, máquina, responsável, prioridade e tipo
- ✅ Atribuição de responsáveis em tempo real
- ✅ Atualização de status: Aberta → Em Andamento → Aguard. Peça → Concluída
- ✅ Histórico completo de ações por OS
- ✅ Filtros por status e busca por texto

### Máquinas
- ✅ Cadastro com setor, modelo e número de patrimônio
- ✅ Histórico completo de OS por máquina

### Responsáveis
- ✅ Cadastro com especialidade, email e telefone

### Dashboard & Relatórios
- ✅ Cards com totais em tempo real
- ✅ Gráfico de barras: OS por máquina
- ✅ Gráfico de rosca: distribuição por status
- ✅ Tabela de desempenho por responsável com taxa de conclusão
- ✅ Linha do tempo dos últimos 7 dias
- ✅ **Tempo Médio de Atendimento** calculado automaticamente
- ✅ Gráficos de tipos de manutenção

## 🔌 API Endpoints

| Método | Rota | Descrição |
|--------|------|-----------|
| GET | /api/ordens | Listar OS (filtros: status, q) |
| POST | /api/ordens | Criar nova OS |
| GET | /api/ordens/:id | Detalhes + histórico |
| PUT | /api/ordens/:id/status | Atualizar status |
| PUT | /api/ordens/:id/atribuir | Atribuir responsável |
| GET | /api/maquinas | Listar máquinas |
| POST | /api/maquinas | Cadastrar máquina |
| GET | /api/maquinas/:id/historico | Histórico da máquina |
| GET | /api/responsaveis | Listar responsáveis |
| POST | /api/responsaveis | Cadastrar responsável |
| GET | /api/dashboard | Dados do dashboard + relatórios |

## 🗄️ Banco de Dados (SQLite)

Tabelas:
- `maquinas` — equipamentos com setor, modelo e patrimônio
- `responsaveis` — técnicos com especialidade e contato  
- `ordens` — ordens de serviço com status e timestamps
- `historico` — log de todas as ações por OS

O banco é criado automaticamente com dados de demonstração na primeira execução.

## 📊 Diferencial: Relatório de Tempo Médio

O sistema calcula automaticamente o **Tempo Médio de Atendimento (TMA)**:

```sql
SELECT AVG((julianday(fechado_at) - julianday(created_at)) * 24) as horas
FROM ordens WHERE status='concluida' AND fechado_at IS NOT NULL
```

Exibido no dashboard principal e na tela de relatórios, com breakdown por responsável.

## 🛠️ Tecnologias

- **Frontend**: HTML5 + CSS3 + JavaScript puro (sem frameworks)
- **Backend**: Python 3 + Flask + Flask-CORS
- **Banco**: SQLite (zero configuração)
- **Fontes**: IBM Plex Sans, IBM Plex Mono, Bebas Neue (Google Fonts)
