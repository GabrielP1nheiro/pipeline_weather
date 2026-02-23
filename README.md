🌦️ Pipeline Weather

Este projeto é uma pipeline de dados climáticos que coleta, processa e armazena informações meteorológicas para cidades específicas, utilizando Apache Airflow e PostgreSQL.

O objetivo é centralizar dados de clima em um banco de dados relacional, permitindo análises e visualizações futuras.



🧩 Tecnologias utilizadas

Python 3.x – Linguagem principal do projeto

Apache Airflow 3.x – Orquestração da pipeline

PostgreSQL 16 – Banco de dados para armazenamento dos dados

Docker & Docker Compose – Containerização da aplicação


<img width="2768" height="970" alt="arquitetura_de_dados_draw" src="https://github.com/user-attachments/assets/edee3fa9-bdb6-46cc-93b1-a31951f6e6a7" />



📦 Como funciona a pipeline

Extração – O script extract_data.py coleta dados climáticos de APIs externas.

Transformação / Normalização – Ajusta dados, formata timestamps e converte tipos.

Carregamento – Salva os dados processados no banco weather_data (tabela sp_weather).

As tarefas estão orquestradas no DAG weather_dag.py.


