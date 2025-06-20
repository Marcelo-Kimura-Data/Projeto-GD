# Projeto - GD

# Arquitetura de Dados: Camadas Bronze, Silver e Gold (Medalhão)

Este repositório implementa uma arquitetura em camadas (conhecida como **"medalhão"**) utilizando Databricks e AWS S3, com o objetivo de estruturar o fluxo de ingestão, tratamento e disponibilização de dados de forma escalável, segura e organizada.

---

## 📌 Estrutura das Camadas

A divisão em camadas ajuda a separar os dados por nível de tratamento, facilitando a manutenção, rastreabilidade e governança.

### 🥉 Camada Bronze – Dados Brutos (Raw Ingestion)

- **Objetivo:** Armazenar os dados exatamente como foram recebidos.
- **Fonte:** Arquivos `.csv` armazenados em bucket S3.
- **Transformações:** Nenhuma ou mínimas (ex: adição de timestamp de carga).
- **Formato:** Delta Lake (`.delta`)


---

### 🥈 Camada Silver – Dados Tratados

- **Objetivo:** Limpar, padronizar e aplicar regras de negócio básicas.
- **Transformações típicas:**
  - Conversão de tipos de dados
  - Remoção de duplicatas
  - Tratamento de nulos e inconsistências
  - Normalização de campos
- **Formato:** Delta Lake
- **Benefício:** Dados prontos para análise exploratória.

---

### 🥇 Camada Gold – Dados Prontos para Consumo

- **Objetivo:** Dados agregados, otimizados e modelados para consumo por ferramentas de BI, APIs ou relatórios.
- **Transformações típicas:**
  - Cálculo de KPIs
  - Agregações
  - Criação de tabelas fato e dimensão
- **Formato:** Delta Lake
- **Benefício:** Alta performance, dados prontos pra contar história (ou salvar o time de negócio).

---

## 🔧 Tecnologias Utilizadas

- **Databricks (Premium)**
- **AWS S3**
- **Delta Lake**
- **PySpark**
- **Unity Catalog**
- **Power BI (consumo final)**

---

## 🧪 Validações e Testes
Validação de Schema em todas as camadas

Testes de Integração entre camadas:

Contagem de registros

Checagem de duplicatas

Validação de IDs presentes entre camadas

---

## 📊 Integração com Power BI
Conexão via conector nativo “Databricks”

Autenticação via JDBC/ODBC
-> Server Hostname + HTTP Path

Consumo direto da camada Gold com tabelas otimizadas em Delta

---

## 🗂️ Versionamento e GitHub

Este projeto utiliza Git para versionamento de código e controle de mudanças.

---

## 📁 Estrutura do Repositório

```bash
├── bronze/
│   └── Bronze_GD.ipynb
├── silver/
│   └── Silver_GD.ipynb
├── gold/
│   └── Gold_GD.ipynb
└── README.md
```


