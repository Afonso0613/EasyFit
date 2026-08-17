<div align="center">

<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0A192F&height=160&section=header&text=EasyFit%20Data%20Warehouse&fontSize=38&fontColor=E6F1FF&animation=fadeIn&fontAlignY=45" />

<br/>

<img src="https://img.shields.io/badge/-Data%20Warehouse-0A192F?style=for-the-badge&logoColor=64FFDA" />
<img src="https://img.shields.io/badge/-Decision%20Support%20System-0A192F?style=for-the-badge&logoColor=64FFDA" />
<img src="https://img.shields.io/badge/-Universidade%20do%20Minho-0A192F?style=for-the-badge&logoColor=64FFDA" />

<br/><br/>

**A dimensional Data Warehouse and decision-support system for EasyFit, a fictional gym**
<br/>
*Sistemas de Armazéns de Dados · Mestrado em Engenharia Informática · 2024/2025*

</div>

<br/>

## About the Project

EasyFit is a modern gym built around self-guided training circuits and free-participation group classes. This project designs and implements a full **Decision Support System (DSS)** on top of a **Data Warehouse**, giving EasyFit's management team the tools to track client engagement, evaluate instructor performance and personalize services based on real usage data.

The system was built end-to-end: requirements gathering, dimensional modelling, ETL pipeline, population, dashboarding and two data mining applications (customer segmentation and a hybrid recommender system).

<br/>

## Key Features

- ⭐ **Star-schema Data Warehouse** modelled with Kimball's 4-step methodology and Golfarelli notation
- 🔄 **ETL pipeline** in Python/pandas loading into MySQL via SQLAlchemy, with three layers of automated testing
- 📊 **5 Power BI dashboards**, each tailored to a specific decision-making profile
- 🧩 **Customer segmentation** via K-Means clustering (6 behavioural/demographic profiles)
- 🎯 **Hybrid recommendation system** (content-based + demographic-collaborative filtering) for personalized training/class suggestions

<br/>

## Data Model

The warehouse follows a **star schema** with two complementary fact tables:

| Fact Table | Grain | Type | Periodicity |
|---|---|---|---|
| `TF-AtividadeCliente` | One gym visit by one client | Transactional | Daily |
| `TF-DesempenhoInstrutor` | One instructor's weekly performance | Aggregated | Weekly |

**Dimensions:** `Dim-Calendário` (role-playing), `Dim-Cliente` (SCD Type 1), `Dim-Campanha` (SCD Type 2), `Dim-Treino` (no variation), `Dim-TipoDeAula` (conformed), `Dim-Instrutor` (SCD Type 1).

<details>
<summary><strong>TF-AtividadeCliente</strong> — measures & dimensions</summary>
<br/>

- **Dimensions:** Cliente, Calendário, Hora (degenerate), Treino, TipoDeAula, Campanha
- **Measures:** Tempo de Permanência (sum), Calorias Queimadas (sum), Avaliação de Treino, Avaliação de Aula

</details>

<details>
<summary><strong>TF-DesempenhoInstrutor</strong> — measures & dimensions</summary>
<br/>

- **Dimensions:** Instrutor, Calendário, TipoDeAula
- **Measures:** Lotação Média, Avaliação Média das Aulas, Avaliação Média dos Treinos, Nº de Planos Seguidos

</details>

<br/>

## Architecture

The system follows a classic layered Data Warehousing architecture:

```
Fontes de Dados → Staging Area (ETL) → Data Warehouse → Data Marts → Dashboards / Data Mining
```

- **Sources:** access control/check-in system, training & class management platform, CRM, mobile app feedback forms
- **Staging Area:** validation, normalization, deduplication and enrichment (e.g. derived visit duration)
- **Warehouse:** MySQL, organized into two thematic Data Marts — *Atividade do Cliente* and *Desempenho do Instrutor*
- **Population:** Python notebooks (pandas + SQLAlchemy), modelled with BPMN, split into three subprocesses (dimensions → client activity facts → instructor performance facts), with referential-integrity, business-rule and plausibility test suites

<br/>

## Dashboards

Five Power BI dashboards, each built for a specific decision agent:

| Dashboard | Audience | Focus |
|---|---|---|
| Utilização e Ocupação | Operations Manager | Attendance patterns, occupancy heatmaps, circuit/class popularity |
| Clientes e Aderência | Client & Loyalty Managers | Attendance trends, demographic breakdowns, churn-risk rankings |
| Campanhas e Marketing | Marketing Manager | Campaign adoption, segmentation by age/profession |
| Desempenho de Instrutores | Instructor Coordinator | Ratings, class occupancy, plan adherence rankings |
| Painel Global de KPIs | Administration | Consolidated business-wide KPIs |

<br/>

## Data Mining

### 🧩 Customer Segmentation
K-Means clustering (k=6, chosen via elbow method + silhouette analysis) on visit frequency, session duration, calories, ratings and demographic/physical attributes (age, BMI). Validated with Silhouette Score (0.135), Davies-Bouldin Index (1.777), and Calinski-Harabasz Score (12.668). Produced six interpretable client profiles, from *"Very Active & Engaged"* to *"Low Engagement & Dissatisfied"*, each with practical retention recommendations.

### 🎯 Recommendation System
A hybrid system combining:
- **Content-based filtering** — cosine similarity between a client's activity profile and available trainings/classes
- **Demographic-collaborative filtering** — similarity between clients based on behavioural + demographic vectors

Evaluated via leave-one-out cross-validation with Precision@3 / Recall@3 / MAP@3 / MRR@3, reaching up to **90% precision and recall** on class recommendations.

<br/>

## Tech Stack

<div align="center">
<img src="https://skillicons.dev/icons?i=python,mysql,figma&theme=dark" />
</div>

<br/>

![Python](https://img.shields.io/badge/-Python-0A192F?style=for-the-badge&logo=python&logoColor=64FFDA)
![Pandas](https://img.shields.io/badge/-Pandas-0A192F?style=for-the-badge&logo=pandas&logoColor=64FFDA)
![scikit-learn](https://img.shields.io/badge/-scikit--learn-0A192F?style=for-the-badge&logo=scikitlearn&logoColor=64FFDA)
![MySQL](https://img.shields.io/badge/-MySQL-0A192F?style=for-the-badge&logo=mysql&logoColor=64FFDA)
![SQLAlchemy](https://img.shields.io/badge/-SQLAlchemy-0A192F?style=for-the-badge&logoColor=64FFDA)
![Power BI](https://img.shields.io/badge/-Power%20BI-0A192F?style=for-the-badge&logo=powerbi&logoColor=64FFDA)
![draw.io](https://img.shields.io/badge/-draw.io-0A192F?style=for-the-badge&logoColor=64FFDA)

<br/>

## Team

Project developed by **Afonso Magalhães**, for the "Sistemas de Armazéns de Dados" specialization profile, Universidade do Minho — May 2025.

<br/>

<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0A192F&height=100&section=footer" />
