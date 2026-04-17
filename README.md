# 🌦️ Pipeline Weather

Pipeline de dados climáticos que coleta, transforma e armazena informações meteorológicas de São Paulo em um banco de dados relacional, com orquestração via Apache Airflow.

---

## 📋 Índice

- [Sobre o Projeto](#-sobre-o-projeto)
- [Arquitetura](#-arquitetura)
- [Tecnologias](#-tecnologias)
- [Estrutura do Repositório](#-estrutura-do-repositório)
- [Pré-requisitos](#-pré-requisitos)
- [Como Executar](#-como-executar)
- [Variáveis de Ambiente](#-variáveis-de-ambiente)
- [Pipeline ETL](#-pipeline-etl)

---

## 📌 Sobre o Projeto

Este projeto implementa uma pipeline ETL (Extract, Transform, Load) para dados climáticos da cidade de São Paulo, utilizando a API do [OpenWeatherMap](https://openweathermap.org/). Os dados coletados são transformados e armazenados em um banco PostgreSQL, com as execuções orquestradas pelo Apache Airflow.

O objetivo é centralizar dados meteorológicos de forma automatizada, viabilizando análises históricas e visualizações futuras.

---

## 🏗️ Arquitetura

```
OpenWeatherMap API
        │
        ▼
   [ Extract ]  ──▶  extract_data.py
        │
        ▼
  [ Transform ] ──▶  transform_data.py
        │
        ▼
    [ Load ]    ──▶  load_data.py
        │
        ▼
  PostgreSQL (tabela: sp_weather)
        │
  (orquestrado por)
        │
   Apache Airflow (weather_dag.py)
```

---

## 🛠️ Tecnologias

| Tecnologia | Versão | Uso |
|---|---|---|
| Python | 3.x | Linguagem principal |
| Apache Airflow | 3.x | Orquestração da pipeline |
| PostgreSQL | 16 | Armazenamento dos dados |
| Docker & Docker Compose | - | Containerização |
| OpenWeatherMap API | 2.5 | Fonte dos dados climáticos |

---

## 📁 Estrutura do Repositório

```
pipeline_weather/
│
├── dags/                   # DAGs do Apache Airflow
│   └── weather_dag.py      # DAG principal da pipeline
│
├── notebooks/              # Análises exploratórias
│
├── src/                    # Módulos da pipeline
│   ├── extract_data.py     # Extração de dados da API
│   ├── transform_data.py   # Transformações e normalização
│   └── load_data.py        # Carregamento no PostgreSQL
│
├── main.py                 # Execução local da pipeline (sem Airflow)
├── docker-compose.yaml     # Configuração dos containers
├── pyproject.toml          # Dependências do projeto
├── .gitignore
└── README.md
```

---

## ✅ Pré-requisitos

- [Docker](https://www.docker.com/) e Docker Compose instalados
- Conta e chave de API no [OpenWeatherMap](https://openweathermap.org/api)
- Python 3.x (para execução local sem Docker)
- [`uv`](https://github.com/astral-sh/uv) para gerenciamento de dependências (opcional)

---

## 🚀 Como Executar

### 1. Clone o repositório

```bash
git clone https://github.com/GabrielP1nheiro/pipeline_weather.git
cd pipeline_weather
```

### 2. Configure as variáveis de ambiente

Crie o arquivo `config/.env` com suas credenciais (veja a seção [Variáveis de Ambiente](#-variáveis-de-ambiente)).

### 3. Suba os containers

```bash
docker-compose up -d
```

### 4. Acesse o Airflow

Após os containers iniciarem, acesse o Airflow em:
```
http://localhost:8080
```
Ative a DAG `weather_dag` para iniciar as execuções agendadas.

### Execução local (sem Airflow)

```bash
pip install -r requirements.txt  # ou: uv sync
python main.py
```

---

## 🔐 Variáveis de Ambiente

Crie o arquivo `config/.env` na raiz do projeto com o seguinte conteúdo:

```env
api_key=SUA_CHAVE_OPENWEATHERMAP

# Conexão PostgreSQL
POSTGRES_USER=seu_usuario
POSTGRES_PASSWORD=sua_senha
POSTGRES_DB=weather_data
POSTGRES_HOST=localhost
POSTGRES_PORT=5432
```

> ⚠️ Nunca suba o arquivo `.env` para o repositório. Ele já está listado no `.gitignore`.

---

## 🔄 Pipeline ETL

A pipeline é composta por três etapas principais:

**1. Extract** — `extract_data.py`
Realiza requisição à API do OpenWeatherMap e coleta dados climáticos de São Paulo (temperatura, umidade, vento, etc.).

**2. Transform** — `transform_data.py`
Normaliza os dados, converte timestamps para o fuso horário correto e adequa os tipos de cada campo.

**3. Load** — `load_data.py`
Salva os dados processados na tabela `sp_weather` do banco PostgreSQL.

---

## 📄 Licença

Este projeto está sob a licença MIT. Consulte o arquivo `LICENSE` para mais detalhes.