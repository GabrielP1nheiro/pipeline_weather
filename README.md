🌦️ Pipeline Weather

Este projeto é uma pipeline de dados climáticos que coleta, processa e armazena informações meteorológicas para cidades específicas, utilizando Apache Airflow e PostgreSQL.

O objetivo é centralizar dados de clima em um banco de dados relacional, permitindo análises e visualizações futuras.

🧩 Tecnologias utilizadas

Python 3.x – Linguagem principal do projeto

Apache Airflow 3.x – Orquestração da pipeline

PostgreSQL 16 – Banco de dados para armazenamento dos dados

Docker & Docker Compose – Containerização da aplicação

Redis – Broker para CeleryExecutor (Airflow)

⚙️ Estrutura do projeto
pipeline_weather/
│
├── dags/                  # DAGs do Airflow
│   └── weather_dag.py
├── src/                   # Scripts de extração, transformação e carregamento
│   ├── extract_data.py
│   ├── transform_data.py
│   └── load_data.py
├── logs/                  # Logs do Airflow
├── plugins/               # Plugins do Airflow (opcional)
├── docker-compose.yaml    # Configuração dos containers
└── README.md              # Documentação do projeto
🚀 Como rodar o projeto
1. Clonar o repositório
git clone https://github.com/GabrielP1nheiro/pipeline_weather.git
cd pipeline_weather
2. Subir containers com Docker Compose
docker compose up -d

Isso vai subir:

Airflow (Scheduler, Webserver, Worker, DAG Processor, Triggerer)

PostgreSQL

Redis

3. Acessar o Airflow

Abra o navegador e acesse:

http://localhost:8080

Usuário e senha padrão:

Username: airflow
Password: airflow
4. Acessar o PostgreSQL

Você pode acessar o banco de dados weather_data via psql ou pgAdmin:

# Exemplo usando psql dentro do container Airflow Worker
docker exec -it pipeline_weather-airflow-worker-1 bash
psql -h host.docker.internal -p 5432 -U airflow -d weather_data

Use o mesmo host e porta no pgAdmin para se conectar:
Host: localhost | Porta: 5432 | Usuário: airflow | Senha: airflow

📦 Como funciona a pipeline

Extração – O script extract_data.py coleta dados climáticos de APIs externas.

Transformação / Normalização – Ajusta dados, formata timestamps e converte tipos.

Carregamento – Salva os dados processados no banco weather_data (tabela sp_weather).

As tarefas estão orquestradas no DAG weather_dag.py.

📝 Observações

Certifique-se de que o .gitignore esteja configurado para não subir logs ou credenciais.

A pipeline está configurada para rodar localmente via Docker; ajustes são necessários para produção.

Alterações nas credenciais do PostgreSQL devem ser refletidas no docker-compose.yaml.
